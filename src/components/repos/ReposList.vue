<template>
  <div class="repos-list">
    <Scrollbar>
      <div class="repos-list__loader-container">
        <img
          class="repos-list__loader-container__loader"
          v-if="isLoading === true"
          src="@/assets/loader.gif"
          alt="loader"
        />
        <div class="repos-list__repo" v-else-if="!error && repos.length > 0">
          <Repo v-for="repo in repos" :key="repo.id" :repo="repo" />
        </div>
        <h1 class="repos-list__comunicat" v-else-if="!error && repos.length === 0">
          Użytkownik nie ma żadnego repo.
        </h1>
        <h1 class="repos-list__comunicat" v-else>{{ error }}</h1>
      </div>
    </Scrollbar>
  </div>
</template>

<script>
import Scrollbar from "../shared/Scrollbar";
import Repo from "./Repo.vue";
export default {
  components: {
    Repo,
    Scrollbar,
  },
  props:['userName'],
  emits: ["isSearchDisabledChange"],
  data() {
    return {
      repos: [],
      error: null,
      isLoading: false,
      isSearchDisabled: false,
      currentUser: "",
    };
  },
  watch:{
    userName: function(user){
     this.displayRepos(user)
    },
    isSearchDisabled: function(state){
      this.$emit("isSearchDisabledChange",state)
    }
  },
  methods: {
    async displayRepos(user) {
      if (user !== this.currentUser) {
        this.isSearchDisabled=true;
        this.isLoading = true;
        this.error = null;
        try {
          const fetchedRepos = await this.fetchRepos(user);
          const processedRepos = this.getProcessedRepos(fetchedRepos);
          this.repos = processedRepos;
          this.isLoading = false;
        } catch (error) {
          this.handleError(error);
        }
        this.isSearchDisabled=false;
        this.currentUser = user;
      }
    },

    async fetchRepos(value) {
      let response = await fetch(`https://api.github.com/users/${value}/repos`);
      if (response.ok) {
        return await response.json();
      } else if (response.status === 404) {
        throw new Error("Nie ma takiego użytkownika");
      } else {
        throw new Error("Coś poszło nie tak, spróbuj ponownie później ;(");
      }
    },

    getProcessedRepos(repos) {
      const processedRepos = [];
      for (const repo of repos) {
        processedRepos.push({
          id: repo.id,
          branch: repo.default_branch,
          description: repo.description,
          name: repo.name,
          photo: repo.owner.avatar_url,
          link: repo.html_url,
          time: new Date(repo.updated_at).getTime(),
        });
      }
      return processedRepos.sort((a, b) => b.time - a.time).reverse();
    },

    handleError(error) {
      this.isLoading = false;
      this.error = error.message;
    },
  },
};
</script>

<style lang="scss" scoped>
.repos-list {
  margin: 0 auto;
  width: 1200px;
  height: 568px;
  overflow: hidden;
  box-shadow: 1px 0px 16px rgba(0, 0, 0, 0.17);
  border-radius: 10px;
  padding: 40px 0;
  &__loader-container {
    display: flex;
    justify-content: flex-start;
    flex-flow: column;
    height: 100%;
    padding: 0 40px;
    &__loader {
      width: 200px;
      height: 200px;
      margin: auto;
    }
  }
  &__comunicat {
      margin: auto;
      color: $primary-color;
    }
  &__repo {
      display: grid;
      grid-template-columns: 1fr 1fr;
      grid-gap: 20px;
    }
}
</style>
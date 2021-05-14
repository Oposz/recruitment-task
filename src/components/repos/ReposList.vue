<template>
  <NavBar />
  <SearchBar @search-repos="searchRepos"></SearchBar>
  <div class="spacer">
    <Scrollbar>
      <div class="box">
        <img
          class="loader"
          v-if="isLoading === true"
          src="../../assets/loader.gif"
          alt="loader"
        />
        <div class="repos" v-else-if="!error">
          <Repo v-for="repo in repos" :key="repo.id" :repo="repo"></Repo>
        </div>
        <h1 v-else>{{ error }}</h1>
      </div>
    </Scrollbar>
  </div>
</template>

<script>
import Scrollbar from "./Scrollbar";
import Repo from "./Repo.vue";
import NavBar from "../design/NavBar.vue";
import SearchBar from "./SearchBar.vue";
export default {
  components: {
    Repo,
    NavBar,
    SearchBar,
    Scrollbar,
  },
  emits: ["searchRepos"],
  data() {
    return {
      repos: [],
      error: null,
      isLoading: false,
      isSearchDisabled: false,
    };
  },
  methods: {
    async searchRepos(user) {
      try {
        this.isSearchDisabled = true;
        this.isLoading = true;
        let response = await fetch(
          `https://api.github.com/users/${user}/repos`
        );
        if (response.ok) {
          let data = await response.json();
          const repo = [];
          for (const id in data) {
            repo.push({
              id: id,
              branch: data[id].default_branch,
              description: data[id].description,
              name: data[id].name,
              photo: data[id].owner.avatar_url,
              link: data[id].html_url,
              time: new Date(data[id].updated_at).getTime(),
            });
          }
          this.repos = repo.sort((a, b) => b.time - a.time);
          this.repos.reverse();
          this.error = null;
          this.isLoading = false;
          this.isSearchDisabled = false;
        } else if (response.status === 404) {
          throw new Error("Nie ma takiego użytkownika.");
        } else {
          throw new Error("Coś poszło nie tak, spróbuj ponownie później ;(");
        }
      } catch (error) {
        this.error = error.message;
        this.isLoading = false;
        this.isSearchDisabled = false;
      }
    },
  },
};
</script>

<style lang="scss" scoped>
.spacer {
  position: absolute;
  width: 1200px;
  height: 568px;
  left: 360px;
  top: 206px;
  overflow: hidden;
  box-shadow: 1px 0px 16px rgba(0, 0, 0, 0.17);
  border-radius: 10px;
  padding: 40px 0;
  .test {
    height: 400;
  }

  .box {
    display: flex;
    justify-content: flex-start;
    flex-flow: column;
    height: 100%;
    padding: 0 40px;
    .loader {
      width: 200px;
      height: 200px;
      margin: auto;
    }
    h1 {
      margin: auto;
      color: #002bdc;
    }
    .repos {
      display: grid;
      grid-template-columns: 1fr 1fr;
      grid-gap: 20px;
    }
  }
}
</style>
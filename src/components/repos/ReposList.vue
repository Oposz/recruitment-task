<template>
  <SearchBar
    @search="displayRepos"
    :defaultUser="defaultUser"
    :instruction="instruction"
    :isSearchDisabled="isSearchDisabled"
  ></SearchBar>
  <div class="spacer">
    <Scrollbar>
      <div class="box">
        <img
          class="loader"
          v-if="isLoading === true"
          src="@/assets/loader.gif"
          alt="loader"
        />
        <div class="repos" v-else-if="!error">
          <Repo v-for="repo in repos" :key="repo.id" :repo="repo" />
        </div>
        <h1 class="error" v-else>{{ error }}</h1>
      </div>
    </Scrollbar>
  </div>
</template>

<script>
import Scrollbar from "./Scrollbar";
import Repo from "./Repo.vue";
import SearchBar from "./SearchBar.vue";
export default {
  components: {
    Repo,
    SearchBar,
    Scrollbar,
  },
  emits: ["search"],
  data() {
    return {
      repos: [],
      error: null,
      isLoading: false,
      isSearchDisabled: false,
      instruction: "Wpisz nazwę użytkownika repo",
      defaultUser: "oposz",
    };
  },
  methods: {

    async displayRepos(user){
      try{
        this.error=null;
        this.isLoading=true;
        const fetchedRepos= await this.fetchRepos(user);
        const processedRepos=await this.getProcessedRepos(fetchedRepos);
        this.repos=processedRepos
        this.isLoading=false;
      }catch(error){
        this.handleError(error);
      }
    },

    async fetchRepos(value){
      let response= await fetch(`https://api.github.com/users/${value}/repos`);
      if(response.ok){
        return await response.json();
      }else if(response.status === 404){
        throw new Error('Nie ma takiego użytkownika')
      }else{
        throw new Error('Coś poszło nie tak, spróbuj ponownie później ;(');
      }
    },

    getProcessedRepos(repos){
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

    handleError(error){
      this.isLoading=false;
      this.error=error.message
    }
  }
}
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
    .error {
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
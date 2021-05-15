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
        const processedRepos=await this.getProcessRapos(fetchedRepos);
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

    getProcessRapos(repos){
      const data=repos;
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
      let sorted = repo.sort((a, b) => b.time - a.time);
      return sorted.reverse();
    },

    handleError(error){
      this.isLoading=false;
      this.error=error.message
    }


  //   sortRepos(repo) {
  //     let sortowane = repo.sort((a, b) => b.time - a.time);
  //     sortowane.reverse();
  //     this.repos=sortowane
  //     this.isLoading=false;
  //     this.isSearchDisabled=false;
  //   },

  //   async renderRepos(data) {
  //     const repo = [];
  //     for (const id in data) {
  //       repo.push({
  //         id: id,
  //         branch: data[id].default_branch,
  //         description: data[id].description,
  //         name: data[id].name,
  //         photo: data[id].owner.avatar_url,
  //         link: data[id].html_url,
  //         time: new Date(data[id].updated_at).getTime(),
  //       });
  //     }
  //     this.sortRepos(repo);
  //   },

  //   async validate(response) {
  //     try {
  //       if (response.status === 404) {
  //         throw new Error("Nie ma takiego użytkownika.");
  //       } else {
  //         throw new Error("Coś poszło nie tak, spróbuj ponownie później ;(");
  //       }
  //     } catch (error) {
  //       this.error = error.message;
  //       this.isLoading=false;
  //       this.isSearchDisabled=false;
  //     }
  //   },

  //   async getPromise(value) {
  //     this.isLoading=true;
  //     this.isSearchDisabled=true;
  //     this.error=null;
  //     await fetch(`https://api.github.com/users/${value}/repos`).then(
  //       (response) => {
  //         if (response.ok) {
  //           return response.json().then((data) => {
  //             this.renderRepos(data);
  //           });
  //         } else {
  //           this.validate(response);
  //         }
  //       }
  //     );
  //   },
  // },
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
<template>
  <NavBar />
  <SearchBar @search-repos="searchRepos"></SearchBar>
  <div class="spacer">
    <div class="box">
      <div class="repos" v-if="!error">
        <Repo v-for="repo in repos" :key="repo.id" :repo="repo"></Repo>
      </div>
      <h1 v-else>{{ error }}</h1>
    </div>
  </div>
</template>

<script>
import Repo from "./Repo.vue";
import NavBar from "../design/NavBar.vue";
import SearchBar from "./SearchBar.vue";
export default {
  components: {
    Repo,
    NavBar,
    SearchBar,
  },
  emits: ["searchRepos"],
  data() {
    return {
      repos: [],
      error: null,
    };
  },
  methods: {
    searchRepos(user) {
      fetch(`https://api.github.com/users/${user}/repos`)
        .then((response) => {
          if (response.ok) {
            return response.json();
          } else if (response.status === 404) {
            throw new Error("Nie ma takiego użytkownika.");
          } else {
            throw new Error("Coś poszło nie tak, spróbuj ponownie później ;(");
          }
        })
        .then((data) => {
          const repo = [];
          for (const id in data) {
            repo.push({
              id: id,
              branch: data[id].default_branch,
              description: data[id].description,
              name: data[id].name,
              photo: data[id].owner.avatar_url,
            });
          }
          this.repos = repo;
          this.error = null;
        })
        .catch((error) => {
          this.error = error.message;
        });
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
  padding-bottom:30px ;
  
  .box {
    display: flex;
    justify-content: flex-start;
    flex-flow: column;
    padding: 40px 39px;
    overflow: auto;
    height: 100%;
    h1 {
      margin: auto;
      color: #002bdc;
    }
    .repos {
      display: grid;
      grid-template-columns: 1fr 1fr;
    }
  }
}

</style>
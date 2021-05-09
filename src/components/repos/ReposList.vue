<template>
  <NavBar></NavBar>
  <SearchBar
  @search-repos="searchRepos"
  ></SearchBar>
  <div class="wrap">
    <Repo
    v-for="repo in repos"
    :key="repo.id"
    :repo="repo"
    :repos="repos"
    ></Repo>
  </div>
</template>

<script>
import Repo from "./Repo.vue"
import NavBar from "../design/NavBar.vue"
import SearchBar from "./SearchBar.vue"
export default {
  
  components:{
    Repo,
    NavBar,
    SearchBar
  },
  emits:['searchRepos'],
  data(){
    return{
      repos:[]
    }
  },
  methods:{
    searchRepos(user){
      fetch(`https://api.github.com/users/${user}/repos`).
      then((response)=>{
        if(response.ok){
          return response.json();
        }
      }).then((data)=>{
        const repo=[]
        for(const id in data){
          repo.push({
            id:id,
            branch:data[id].default_branch,
            description:data[id].description,
            name:data[id].name,
            photo:data[id].owner.avatar_url
          })
        }
        this.repos=repo
        
      })//catch
    }
  }
};
</script>

<style lang="scss" scoped>
.wrap{
  position: absolute;
  width: 1200px;
  height: 568px;
  left: 360px;
  top: 206px;
  display: flex;
  justify-content: flex-start;
  flex-flow: column;
  box-shadow: 1px 0px 16px rgba(0, 0, 0, 0.17);
border-radius: 10px;
padding-top: 20px;
}
</style>
<template>
  <Header 
  @passSearch="getValue"
  :isSearchDisabled="isSearchDisabled"
  />
  <ReposList 
  :userName="userName"
  @isSearchDisabledChange="handleIsSearchDisabledChange"
  />
</template>

<script>
import ReposList from "./components/repos/ReposList.vue";
import Header from "./components/design/Header.vue";

export default {
  components: {
    ReposList,
    Header,
  },
  
  data(){
    return{
      userName:"",
      isSearchDisabled:false,
    };
  },
  methods:{
    getValue(value){
      this.userName=value
    },
    handleIsSearchDisabledChange(state){
      this.isSearchDisabled=state
    }
  }
};
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css?family=Roboto:400,500,700&display=swap");
* {
  font-family: Roboto;
  box-sizing: border-box;
  
}
body {
  margin: 0;
}
</style>

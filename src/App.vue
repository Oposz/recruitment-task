<template>
  <Logo></Logo>
  <NavBar></NavBar>
  <ReposList></ReposList>
</template>

<script>
import NavBar from "./components/design/NavBar.vue";
import Logo from "./components/design/Logo.vue";
import ReposList from "./components/repos/ReposList.vue";
export default {
  components: {
    NavBar,
    Logo,
    ReposList,
  },
  data(){
    return{
      
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

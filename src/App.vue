<template>
  <Logo></Logo>
  <NavBar></NavBar>
  <ReposList></ReposList>
</template>

<script>
import NavBar from "./components/NavBar.vue";
import Logo from "./components/Logo.vue";
import ReposList from "./components/ReposList.vue";
export default {
  components: {
    NavBar,
    Logo,
    ReposList,
  },
};
</script>

<style >
@import url("https://fonts.googleapis.com/css?family=Roboto:400,500,700&display=swap");

* {
  font-family: Roboto;
  box-sizing: border-box;
}
body {
  margin: 0;
}
</style>

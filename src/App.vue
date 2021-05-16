<template>
  <Header />
  <ReposList />
</template>

<script>
import ReposList from "./components/repos/ReposList.vue";
import Header from "./components/design/Header.vue";

export default {
  components: {
    ReposList,
    Header,
  },
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

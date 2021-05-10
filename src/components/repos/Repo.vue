<template>
  <div class="wrapper">
    <img :src="repo.photo" alt="zdjęcie" />
    <div class="inside_wrapper">
      <h2>{{ repo.name }}</h2>
      <p class="description">{{ repo.description }}</p>
      <p class="branch">{{ repo.branch }}</p>
    </div>
    <Arrow></Arrow>
  </div>
</template>

<script>
import Arrow from "../design/Arrow.vue"
export default {
  components:{
    Arrow,
  },
  props: ["repo", "key", "repos"],
  data() {
    return {};
  },
};
</script>

<style lang="scss" scoped>
.wrapper {
  display: flex;
  justify-content: space-evenly;
  margin: 20px 20px 0px 39px;
  width: 555px;
  height: 130px;
  & img {
    width: 60px;
    height: 60px;
    border-radius: 50%;
    object-fit: cover;
  }
  & .inside_wrapper {
    display: flex;
    flex-flow: column;
    justify-content: space-evenly;
    & h2 {
      margin: 0;
    }
    & .description {
      font-style: normal;
      font-weight: normal;
      font-size: 16px;
      line-height: 20px;
      margin: 0;
    }
    & .branch {
      font-style: normal;
      font-weight: normal;
      font-size: 10px;
      line-height: 12px;
      margin: 0;
    }
  }
}
</style>

<template>
  <div class="wrapper">
    <img :src="repo.photo" alt="zdjęcie" class="photo" />
    <div class="inside_wrapper">
      <h2>{{ repo.name }}</h2>
      <p class="description">{{ repo.description ?? "Brak opisu" }}</p>
      <p class="branch">{{ repo.branch }}</p>
    </div>
    <Arrow />
  </div>
</template>

<script>
import Arrow from "../design/Arrow.vue";
export default {
  components: {
    Arrow,
  },
  props: ["repo"],
  data() {
    return {};
  },
};
</script>

<style lang="scss" scoped>
.wrapper {
  display: flex;
  align-items: flex-start;
  width: 555px;
  height: 130px;
  margin: 0 20px 20px 0;
  padding: 26px 30px 13px 30px;
  background-color: #f1f4ff;
  border-radius: 10px;
  .photo {
    width: 60px;
    height: 60px;
    border-radius: 50%;
    object-fit: cover;
  }
  .inside_wrapper {
    display: flex;
    flex-flow: column;
    margin: 0 20px;
    h2 {
      margin: 0;
      color: #304389;
    }
    .description {
      font-style: normal;
      font-weight: normal;
      font-size: 16px;
      line-height: 20px;
      color: #848484;
      margin: 0;
    }
    .branch {
      font-style: normal;
      font-weight: normal;
      font-size: 10px;
      line-height: 12px;
      color: #a5b8ff;
      margin: 0;
    }
  }
}
</style>

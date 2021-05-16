<template>
  <div class="wrapper">
    <img :src="repo.photo" alt="zdjęcie" class="photo" />
    <div class="inside_wrapper">
      <h4 class="repo_name">{{ repo.name }}</h4>
      <p class="description">{{ repo.description ?? "Brak opisu" }}</p>
      <p class="branch">{{ repo.branch }}</p>
    </div>
    <a class="repo_link" target="_blank" :href="repo.link">
      <img src="@/assets/arrow.svg" alt="przejdź do repo" />
    </a>
  </div>
</template>

<script>
export default {
  props: ["repo"],
};
</script>

<style lang="scss" scoped>
.wrapper {
  display: flex;
  align-items: flex-start;
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
    overflow: hidden;
    width: 340px;
    margin: 0 20px;
    .repo_name {
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
      text-overflow: ellipsis;
      white-space: nowrap;
      overflow: hidden;
    }
    .branch {
      font-style: normal;
      font-weight: normal;
      font-size: 10px;
      line-height: 12px;
      color: #a5b8ff;
      margin-bottom: auto;
    }
  }
  .repo_link {
    width: 34px;
    height: 34px;
    align-self: center;
  }
}
</style>

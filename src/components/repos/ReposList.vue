<template>
  <div class="wrap">
    <Repo></Repo>
  </div>
</template>

<script>
import Repo from "./Repo.vue"
export default {
  components:{
    Repo,
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
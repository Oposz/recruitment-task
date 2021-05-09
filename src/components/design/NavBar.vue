<template>
  <div>
    <p>{{ header }}</p>
    <SearchBar></SearchBar>
  </div>
</template>

<script>
import SearchBar from "../repos/SearchBar.vue";

export default {
  components: {
    SearchBar,
  },
  data() {
    return {
      header: "Rekrutacja GBX Soft",
    };
  },
};
</script>
<style lang="scss" scoped>
p {
  position: absolute;
  width: 528px;
  height: 71px;
  left: 360px;
  top: 119px;
  font-style: normal;
  font-weight: bold;
  font-size: 48px;
  line-height: 56px;
  color: #002bdc;
  margin:0;
}
</style>
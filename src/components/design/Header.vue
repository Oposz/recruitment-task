<template>
  <div>
    <p class="header">{{ header }}</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      header: "Rekrutacja GBX Soft",
    };
  },
};
</script>
<style lang="scss" scoped>
.header {
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
  margin: 0;
}
</style>
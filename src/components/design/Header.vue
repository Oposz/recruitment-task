<template>
  <Logo />
  <div>
    <h1 class="header">Rekrutacja GBX Soft</h1>
  </div>
</template>

<script>
import Logo from "./Logo.vue";
export default {
  components: {
    Logo,
  },
};
</script>

<style lang="scss" scoped>
$text-color: #002bdc;
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
  color: $text-color;
  margin: 0;
}
</style>
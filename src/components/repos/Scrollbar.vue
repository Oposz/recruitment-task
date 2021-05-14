<template>
  <div ref="scrollwrap" style="height: 100%">
    <slot> </slot>
  </div>
</template>

<script>
import SimpleBar from "simplebar";
export default {
  data() {
    return {
      simplebar: null,
    };
  },
  mounted() {
    this.simplebar = new SimpleBar(this.$refs.scrollwrap, {
      autoHide: false,
    });
  },
  unmounted() {
    this.simplebar.unMount();
  },
};
</script>

<style lang="scss">
.simplebar-content-wrapper {
  overflow: auto;
}
.simplebar-track.simplebar-vertical {
  border-radius: 50px;
  background: #e1e1e1;
  width: 4px !important;
  margin-top: -8px;
  margin-bottom: -8px;
  right: 12px;
  .simplebar-scrollbar {
    background: #a8a8a8;
    border-radius: 50px;
  }
}
</style>
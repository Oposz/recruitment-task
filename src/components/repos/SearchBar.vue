<template>
  <div class="container">
    <p class="instruction">{{ instruction }}</p>
    <div class="input_wrapper">
      <input
        type="text"
        class="user_input"
        :placeholder="defaultUser"
        @keydown.enter="search()"
        v-model="value"
        :disabled="isSearchDisabled"
      />
      <img
        class="arrow"
        :class="{ visible: value !== '' }"
        src="@/assets/arrow.svg"
        alt="strzałka"
        @click="search()"
      />
    </div>
  </div>
</template>

<script>
export default {
  props: ["isSearchDisabled", "defaultUser", "instruction"],
  data() {
    return {
      value: "",
      focus: false,
    };
  },
  methods: {
    search() {
      if(!this.isSearchDisabled){
        this.$emit("search", this.value);
      }
    },
  },
};
</script>

<style lang="scss" scoped>
.container {
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  position: absolute;
  width: 393px;
  height: 62px;
  left: 1167px;
  top: 119px;

  .instruction {
    color: #304389;
    margin: 0 0 0 8px;
    font-style: normal;
    font-weight: normal;
    font-size: 12px;
    line-height: 18px;
  }
  .input_wrapper {
    .user_input {
      -webkit-appearance: none;
      -moz-appearance: none;
      appearance: none;
      background: #ffffff;
      border: 2px solid #f1f4ff;
      box-sizing: border-box;
      border-radius: 10px;
      font-size: 18px;
      line-height: 18px;
      height: 42px;
      width: 100%;
      padding: 5px;
    }

    .arrow {
      position: absolute;
      width: 17px;
      height: 16px;
      top: 33px;
      left: 350px;
      visibility: hidden;
      cursor: pointer;
      &.visible {
        visibility: visible;
      }
    }
  }
}
</style>
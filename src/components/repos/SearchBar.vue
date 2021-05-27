<template>
  <div class="searchbar">
    <p class="searchbar__instruction">{{ instruction }}</p>
    <div class="searchbar__inside-wrapper">
      <input
        type="text"
        class="searchbar__inside-wrapper__user-input"
        :placeholder="defaultUser"
        @keydown.enter="search()"
        v-model="value"
        :disabled="isSearchDisabled"
      />
      <img
        class="searchbar__inside-wrapper__user-input-button"
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
  emits:["search"],
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
.searchbar {
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  width: 393px;
  height: 62px;

  &__instruction {
    color: #304389;
    margin: 0 0 0 8px;
    font-style: normal;
    font-weight: normal;
    font-size: 12px;
    line-height: 18px;
  }
  &__inside-wrapper {
    &__user-input {
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
    &__user-input-button {
      position: relative;
      bottom:29px;
      left: 360px;
      width: 17px;
      height: 16px;
      visibility: hidden;
      cursor: pointer;
      &.visible {
        visibility: visible;
      }
    }
  }
}
@media (max-width:1199px) {
  .searchbar__inside-wrapper__user-input-button{
    visibility: hidden !important;
  }
}
</style>
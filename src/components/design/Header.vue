<template>
  <div class="header">
    <div class="header__container">
      <div class="header__container__logo">
        <Logo />
      </div>
      <div class="header__title">
        <h1 class="title">Rekrutacja GBX Soft</h1>
      </div>
    </div>
    <div class="header__searchbar">
      <div class="header__searchbar__position">
        <SearchBar
          @search="passSearch"
          :defaultUser="defaultUser"
          :instruction="instruction"
          :isSearchDisabled="isSearchDisabled"
        />
      </div>
    </div>
  </div>
</template>

<script>
import Logo from "./Logo.vue";
import SearchBar from "../repos/SearchBar.vue";
export default {
  components: {
    Logo,
    SearchBar,
  },
  emits: ["passSearch"],
  props: ["isSearchDisabled"],
  data() {
    return {
      instruction: "Wpisz nazwę użytkownika repo",
      defaultUser: "oposz",
    };
  },
  methods: {
    passSearch(value) {
      this.$emit("passSearch", value);
    },
  },
};
</script>

<style lang="scss" scoped>
.header {
  margin: 0 auto;
  max-width: 1200px;
  display: flex;
  justify-content: space-between;

  &__container {
    display: flex;
    flex-flow: column;

    &__logo {
      margin: 30px 0 46px 0;
    }
    .title {
      width: 528px;
      height: 71px;
      font-style: normal;
      font-weight: bold;
      font-size: 48px;
      line-height: 56px;
      color: $primary-color;
      margin: 0 0 16px 0;
    }
  }
  &__searchbar {
    margin-top: auto;

    &__position{
      margin-bottom: 25px;
    }
  }
}
</style>
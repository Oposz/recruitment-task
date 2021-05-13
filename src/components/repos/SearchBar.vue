<template>
  <div class="container">
    <p>Wpisz nazwę użytkownika repo</p>
    <div class="input_wrapper"
    :class="isSearchDisabled ? disabled:null"
    >
      <input
        type="text"
        placeholder="oposz"
        @keydown.enter="searchRepos"
        v-model="user"
        @focus="toggleVisibility"
        @focusout="toggleVisibilityAfter"
        :disabled="isSearchDisabled"
      />
      <img
        class="search"
        src="../../assets/arrow.svg"
        alt="strzałka"
        @click="searchRepos()"
        :style="{visibility: focus? 'visible':'hidden'}" 
      />
    </div>
  </div>
</template>

<script>
export default {
  props:['isSearchDisabled'],
  data() {
    return {
      user: "",
      focus:false,
      };
  },
  methods: {
    searchRepos() {
      this.$emit("search-repos", this.user);
    },
   toggleVisibility(){
     this.focus=!this.focus
   },
   toggleVisibilityAfter(){
     setTimeout(() => {
       this.focus=!this.focus
     },110);
   }
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

  p {
    color: #304389;
    margin: 0 0 0 8px;
    font-style: normal;
    font-weight: normal;
    font-size: 12px;
    line-height: 18px;
  }
  .input_wrapper {
    input {
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

    .search {
      position: absolute;
      width: 17px;
      height: 16px;
      top: 33px;
      left: 350px;
      visibility: hidden;
      cursor:pointer;
    }
  }
}
</style>
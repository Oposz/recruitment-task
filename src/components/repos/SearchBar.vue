<template>
  <div class="container">
    <p>Wpisz nazwę użytkownika repo</p>
    <div class="input_wrapper">
      <input
        type="text"
        placeholder="oposz"
        @keydown.enter="searchRepos()"
        v-model="user"
      />
      <img
        src="../../assets/arrow.svg"
        alt="strzałka"
        @click="searchRepos()"
        
      />
    </div>
  </div>
</template>

<script>
// import Arrow from "../design/Arrow.vue";
export default {
  components: {
    // Arrow,
  },
  data() {
    return {
      user: "",
      focus: false,
    };
  },
  methods: {
    searchRepos() {
      this.$emit("search-repos", this.user);
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

    img {
      position: absolute;
      width: 17px;
      height: 16px;
      top: 33px;
      left: 350px;
      visibility: hidden;
    }
  }
}
</style>
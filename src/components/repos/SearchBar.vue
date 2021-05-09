<template>
  <div>
    <p>Wpisz nazwę użytkownika repo</p>
    <input type="text" placeholder="oposz" />
  </div>
</template>

<script>
export default {};
</script>

<style lang="scss" scoped>
div {
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  position: absolute;
  width: 393px;
  height: 62px;
  left: 1167px;
  top: 119px;

  & p {
    color: #304389;
    margin: 0 0 0 8px;
    font-style: normal;
    font-weight: normal;
    font-size: 12px;
    line-height: 18px;
  }
  & input {
    -webkit-appearance:none;
    -moz-appearance:none;
    appearance:none;
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
}
</style>
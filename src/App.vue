<template>
  <div class="container">
    <validator-input />
    <buildings-list />
  </div>
</template>

<script>
import buildingsList from "./components/buildingsList";
import validatorInput from "./components/validatorInput";

export default {
  name: "App",
  components: {
    buildingsList,
    validatorInput,
  },
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

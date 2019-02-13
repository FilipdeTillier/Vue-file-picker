<template>
  <div id="app">
    <file-picker></file-picker>
  </div>
</template>

<script>
import FilePicker from "./components/file-picker/FilePicker.vue";

export default {
  name: "app",
  components: {
    FilePicker
  }
};
</script>

<style lang="scss">
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

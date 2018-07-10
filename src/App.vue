<template>
  <div id="app">
    <q-card></q-card>
  </div>
</template>

<script>
import qCard from "./components/questionCard";

export default {
  name: "app",
  data() {
    return {};
  },
  components: {
    qCard
  }
};
</script>

<style>
#app {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}
body {
  background-color: aliceblue;
  margin: 0;
}
</style>

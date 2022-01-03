<template>
  <div id="app">
    <VuelidateForm />
  </div>
</template>

<script>
import VuelidateForm from "./components/VuelidateForm.vue";
export default {
  name: "App",
  components: {
    VuelidateForm,
  },
};
</script>

<style>
body {
  margin: 0;
  width: 100%;
  height: 100vh;
}
#app {
  width: 100%;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>

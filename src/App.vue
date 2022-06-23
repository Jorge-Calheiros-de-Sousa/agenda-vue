<template>
  <div id="app">
    <agenda />
  </div>
</template>

<script>
import Agenda from "./main/Agenda.vue";

export default {
  name: "App",
  components: { Agenda },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
}
</style>

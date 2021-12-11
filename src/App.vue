<template>
  <!-- <img alt="Vue logo" src="./assets/logo.png" /> -->
  <GamePair/>
</template>

<script>
import GamePair from "./game/GamePair.vue";

export default {
  name: "App",
  components: {
    GamePair,
  },
};
</script>

<style lang="scss">
body   {
  background-color: #2c3e50;
  color: #fff;
  margin: 0;  
  height: 100vh;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>

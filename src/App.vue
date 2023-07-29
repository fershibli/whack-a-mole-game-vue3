<template>
  <div id="app">
    <h1>Whack-a-Mole Game</h1>
    <HelloWorld ref="game" />
    <button @click="startGame" v-if="!gameStarted">Start Game</button>
  </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";

export default {
  components: {
    HelloWorld,
  },
  data() {
    return {
      gameStarted: false,
    };
  },
  methods: {
    startGame() {
      this.$refs.game.startGame();
      this.gameStarted = true;
    },
  },
};
</script>

<template>
  <div class="game-container">
    <div class="hole" v-for="(mole, index) in moles" :key="index">
      <div class="mole" v-if="mole.show" @click="whack(index)"></div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      moles: Array(9).fill({ show: false }), // 9 holes for moles
      score: 0,
      timeLeft: 30, // 30 seconds game time
      intervalId: null,
    };
  },
  methods: {
    startGame() {
      this.resetGame();
      this.intervalId = setInterval(() => {
        this.timeLeft--;
        if (this.timeLeft <= 0) {
          clearInterval(this.intervalId);
          alert(`Game Over! Your score: ${this.score}`);
        }
      }, 1000);

      this.showRandomMole();
    },
    resetGame() {
      this.moles.forEach((mole) => (mole.show = false));
      this.score = 0;
      this.timeLeft = 30;
    },
    showRandomMole() {
      const index = Math.floor(Math.random() * this.moles.length);
      this.moles[index].show = true;

      setTimeout(() => {
        this.moles[index].show = false;
        this.showRandomMole();
      }, 800 + Math.random() * 500);
    },
    whack(index) {
      if (this.moles[index].show) {
        this.moles[index].show = false;
        this.score++;
      }
    },
  },
};
</script>

<style>
.game-container {
  display: flex;
  flex-wrap: wrap;
  width: 400px;
  margin: 0 auto;
}

.hole {
  position: relative;
  width: 100px;
  height: 100px;
  background-color: #3e2723;
  margin: 10px;
}

.mole {
  position: absolute;
  width: 80px;
  height: 80px;
  background-color: #9c786c;
  border-radius: 50%;
  top: 10px;
  left: 10px;
  display: flex;
  justify-content: center;
  align-items: center;
  cursor: pointer;
  transition: top 0.2s ease;
}

.mole:hover {
  top: 0;
}
</style>

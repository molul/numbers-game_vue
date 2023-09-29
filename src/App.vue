<template>
  <div class="text-center max-w-lg mx-auto bg-slate-700 min-h-screen p-2">
    <!-- Title -->
    <Header />

    <div v-if="status === 'beginning'">
      <Start @start-game="startGame" />
    </div>

    <div
      v-if="status === 'gaming'"
      class="height-100 d-flex justify-content-center align-items-center"
    >
      <Game :size="size" @stop-game="stopGame" @play-again="playAgain" />
    </div>

    <div
      v-if="status === 'stopping'"
      class="height-100 d-flex justify-content-center align-items-center"
    >
      <PlayAgain :score="score" :record="record" @play-again="playAgain" />
    </div>

    <Footer />
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import Footer from "./components/Footer.vue";
import Start from "./components/Start.vue";
import Game from "./components/Game.vue";
import PlayAgain from "./components/PlayAgain.vue";

export default {
  name: "AppComponent",
  components: { Header, Footer, Start, Game, PlayAgain },
  data() {
    return {
      size: 3,
      status: "beginning",
      score: 0,
      record: Infinity,
    };
  },
  methods: {
    startGame(size) {
      this.size = size;
      this.status = "gaming";
    },
    stopGame(score) {
      this.status = "stopping";
      this.score = score;
      if (this.score < this.record) {
        this.record = this.score;
      }
    },
    playAgain() {
      this.status = "beginning";
    },
  },
};
</script>

<style>
.height-100 {
  height: 100vh;
}
</style>

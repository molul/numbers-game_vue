<template>
  <div class="text-center py-4 rounded-lg bg-slate-300">
    <div class="text-3xl font-bold mb-4">You won!</div>

    <div class="mb-4">
      <div>Time: <Time :time="score" /></div>
      <div>Best time: <Time :time="record" /></div>
    </div>

    <div>
      <button
        class="text-sm sm:text-base shadow-md transition-colors px-6 py-2 rounded-md bg-slate-500 hover:bg-slate-400 active:bg-slate-400 text-white"
        @click="$emit('play-again')"
      >
        Play again
      </button>
    </div>
  </div>
</template>

<script>
import Time from "./Time.vue";

export default {
  name: "PlayAgainComponent",
  props: ["score", "record"],
  components: { Time },
};
</script>

<style scoped>
h3 {
  margin: 0;
}
</style>

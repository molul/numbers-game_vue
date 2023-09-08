<template>
	<div class="text-center py-4 rounded-lg bg-slate-300">
		<div class="text-xl font-bold mb-2">Choose level</div>
		<div>
			<input type="radio" name="level" id="easy" :value="3" v-model="level" checked />
			<label for="easy" class="me-4">Easy</label>

			<input type="radio" name="level" :value="4" id="medium" v-model="level"  />
			<label for="medium" class="me-4">Medium</label>

			<input type="radio" name="level" :value="5" id="hard" v-model="level" />
			<label for="hard">Hard</label>
		</div>

		<div class="mt-4">
			<button class="text-sm sm:text-base shadow-md transition-colors px-6 py-2 rounded-md bg-slate-500 hover:bg-slate-400 active:bg-slate-400 text-white " @click="$emit('start-game', this.level)">START</button>
		</div>
	</div>
</template>

<script>
export default {
	name: "StartComponent",
	data() {
		return {
			level: 3,
		}
	}
};
</script>

<style>
label {
  font-size: 18px;
}

button {
  padding: 10px 35px !important;
  font-size: 20px !important;
}

input {
  margin-right: 10px !important;
}
</style>
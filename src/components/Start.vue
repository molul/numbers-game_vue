<template>
	<div class="text-center py-6 rounded-lg bg-slate-300">
		<div class="text-xl font-bold mb-4">Choose level</div>
		
		<div class="px-2 sm:px-4 space-y-6">
			<div class="">
				<button class="w-2/3 h-14 text-sm sm:text-base shadow-md transition-colors px-6 py-2 rounded-md bg-slate-500 hover:bg-slate-400 active:bg-slate-400 text-white " @click="$emit('start-game', 3)">Easy (3x3)</button>
			</div>

			<div class="">
				<button class="w-2/3 h-14 text-sm sm:text-base shadow-md transition-colors px-6 py-2 rounded-md bg-slate-500 hover:bg-slate-400 active:bg-slate-400 text-white " @click="$emit('start-game', 4)">Medium (4x4)</button>
			</div>

			<div class="">
				<button class="w-2/3 h-14 text-sm sm:text-base shadow-md transition-colors px-6 py-2 rounded-md bg-slate-500 hover:bg-slate-400 active:bg-slate-400 text-white " @click="$emit('start-game', 5)">Hard (5x5)</button>
			</div>
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
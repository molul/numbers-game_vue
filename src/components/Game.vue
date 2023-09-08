<template>
	<div class="text-left p-4 rounded-lg bg-slate-300">
		<div class="mb-3 flex gap-3 items-center">
			<div class="font-bold">Time</div>
			<div class="bg-slate-700 text-white rounded p-2 w-full">
				<Time :time="time"/>
			</div>
		</div>

		<div class="relative shadow-md shadow-slate-500/50 max-w-lg rounded-md bg-slate-200 mx-auto space-y-2 p-4 sm:p-6">
			<div class="max-w-lg flex items-center justify-center space-x-1" v-for="(i, row) in board" :key="i">
				<div class=" text-white text-2xl font-bold inline-block w-40 aspect-square rounded sm:rounded-md flex items-center justify-center bg-slate-500 shadow-lg" v-for="(j, col) in i" :key="j" @click="swapBoard(row, col)">
					{{ j }}
				</div>
			</div>
		</div>

		<div class="text-center mt-4">
			<button class="text-sm sm:text-base shadow-md transition-colors px-6 py-2 rounded-md bg-slate-500 hover:bg-slate-400 active:bg-slate-400 text-white " @click="$emit('play-again')">Restart</button>
		</div>

	</div>
</template>

<script>
import Time from './Time.vue';
import { createBoard, mixBoard, isSwappable, getSwappableIndexes, swap, isCorrectBoard } from '../functions';

export default {
	name: 'GameComponent',
	props: ["size"],
	components: { Time },
	data() {
		return {
			board: [],
			time: 0,
			intervalId: 0,
		}
	},
	created() {
		this.board = createBoard(this.size);
		this.board = mixBoard(this.board, 1000);
		this.intervalId = setInterval(() => this.time++, 10);
	},
	unmounted() {
		clearInterval(this.intervalId);
	},
	methods: {
		swapBoard (i, j) {
			if (isSwappable(this.board, [i, j])) {
				const indexes = getSwappableIndexes(this.board, [i, j]);
				this.board = swap(this.board, indexes[0], indexes[1]);
			}
			if (isCorrectBoard(this.board)) {
				this.$emit('stop-game', this.time);
			}
		}
	}
}
</script>

<style>
td {
  width: 80px;
  height: 80px;
  font-size: 40px;
  border: 2px solid #000 !important;
  text-align: center;

  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

td:hover {
  cursor: pointer;
}
</style>

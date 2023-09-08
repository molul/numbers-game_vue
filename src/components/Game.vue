<template>
	<div class="text-left p-4 rounded-lg bg-slate-300">
		<div class="mb-3">
			<Time :time="time"/>
		</div>

		<div class="relative shadow-md shadow-slate-500/50 max-w-lg rounded-md bg-slate-300 mx-auto space-y-2 p-4 sm:p-6">
					<div class="max-w-lg flex items-center justify-center space-x-1" v-for="(i, row) in board" :key="i">
						<div class=" text-white text-2xl font-bold inline-block w-20 aspect-square rounded sm:rounded-md flex items-center justify-center bg-slate-400 shadow-lg" v-for="(j, col) in i" :key="j" @click="swapBoard(row, col)">
							{{ j }}
						</div>
					</div>
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

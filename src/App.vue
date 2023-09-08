<template>
	<div class="text-center max-w-lg mx-auto bg-slate-700 min-h-screen p-2">
		<!-- Title -->
		<div class="p-4 mt-2 mb-4 rounded-md bg-slate-500 mx-auto shadow-md shadow-slate-800/50 text-left">
			<div class="text-xl sm:text-3xl font-bold text-white flex justify-left items-center gap-4">
				<div class="w-10">
					<img src="/vue.png" alt="angular_icon" />
				</div>
				<div >
					NUMBERS PUZZLE GAME
				</div>
			</div>
		</div>


		<div v-if="status === 'beginning'">
			<Start @start-game="startGame"/>
		</div>

		<div v-if="status === 'gaming'" class="height-100 d-flex justify-content-center align-items-center">
			<Game :size="size" @stop-game="stopGame"/>
		</div>

		<div v-if="status === 'stopping'" class="height-100 d-flex justify-content-center align-items-center">
			<PlayAgain :score="score" :record="record" @play-again="playAgain"/>
		</div>
	</div>
</template>

<script>
import Start from './components/Start.vue';
import Game from './components/Game.vue';
import PlayAgain from './components/PlayAgain.vue';

export default {
	name: "AppComponent",
	components: { Start, Game, PlayAgain },
	data (){
		return {
			size: 3,
			status: 'beginning',
			score: 0,
			record: Infinity,
		};
	},
	methods: {
		startGame(size) {
			this.size = size;
			this.status = 'gaming';
		},
		stopGame(score) {
			this.status = 'stopping';
			this.score = score;
			if (this.score < this.record) {
				this.record = this.score
			}
		},
		playAgain () {
			this.status = 'gaming';
		}
	}
}
</script>

<style>
.height-100 {
	height: 100vh;
}

</style>
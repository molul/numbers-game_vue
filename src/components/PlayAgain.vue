<template>
	<div class="text-center">
		<div>
			<h3>Time: <Time :time="score" /></h3>
			<h3>Best time: <Time :time="record" /></h3>
		</div>
		<div>
			<button class="btn btn-secondary mt-4" @click="$emit('play-again')">Play again</button>
		</div>
	</div>
	
</template>

<script>
import Time from './Time.vue';

export default {
	name: 'PlayAgainComponent',
	props: [ 'score', 'record' ],
	components: {Time},
}
</script>

<style scoped>
h3 {
	margin: 0;
}
</style>
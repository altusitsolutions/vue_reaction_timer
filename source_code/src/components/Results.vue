<template>
	<div class="resultsBox">
		<div v-if="!oops">
			<span class="reactionTime">Your reaction time is {{ score }}ms</span><br />
			<span class="rank">{{ rank }}</span>
			<br /><br />
		</div>
		<div v-if="oops">
			<span class="reactionTime">Don't be impatient...</span>
		</div>
	</div>
</template>

<script>
	export default {
		props: ['score', 'oops'],
		data() {
			return {
				rank: null,
			}
		},
		mounted() {
			if (this.score < 250) {
				this.rank = 'Nimble Fingers'
			} else if (this.score < 400) {
				this.rank = 'Meh...'
			} else {
				this.rank = 'Were you even paying attention?'
			}
		},
	}
</script>

<style scoped>
	.rank {
		font-size: 0.5em;
		text-decoration: underline;
	}
</style>

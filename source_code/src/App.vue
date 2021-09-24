<template>
	<h1>Reaction Timer</h1>
	<div @click="start" v-if="showButton" class="playButton block">
		<Results :score="score" v-if="showResults" :oops="oops" />
		<span class="playAgain">Play Again</span>
	</div>
	<Block v-if="isPlaying" :delay="delay" @end="endGame" @impatient="tooSoon" />
</template>

<script>
	import Block from './components/Block.vue'
	import Results from './components/Results.vue'

	export default {
		name: 'App',
		components: {
			Block,
			Results,
		},
		data() {
			return {
				isPlaying: false,
				showButton: true,
				delay: null,
				score: null,
				oops: false,
				showResults: false,
			}
		},
		methods: {
			start() {
				this.delay = 1000 + Math.random() * 5000
				this.isPlaying = true
				this.showResults = false
				this.showButton = false
				this.oops = false
			},
			endGame(reactionTime) {
				this.score = reactionTime
				this.isPlaying = false
				this.showResults = true
				this.showButton = true
				this.oops = false
			},
			tooSoon(earlyClick) {
				this.oops = earlyClick
				this.isPlaying = false
				this.showResults = true
				this.showButton = true
			},
		},
	}
</script>

<style>
	#app {
		font-family: Avenir, Helvetica, Arial, sans-serif;
		-webkit-font-smoothing: antialiased;
		-moz-osx-font-smoothing: grayscale;
		text-align: center;
		color: #505050;
		margin-top: 60px;
	}

	body {
		margin: 0;
	}

	.playAgain {
		font-weight: 600;
		font-size: 0.8em;
	}

	.block {
		width: 100%;
		background: #029302;
		color: #fff;
		text-align: center;
		padding: 100px 0;
		border: none;
		cursor: pointer;
		font-size: 3em;
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		height: 300px;
	}
	.block.redBlock {
		background: crimson;
	}
</style>

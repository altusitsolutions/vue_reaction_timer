<template>
	<div class="redBlock block" v-if="showRedBlock" @click="tooSoon">
		<span>Wait...</span>
	</div>
	<div class="greenBlock block" v-if="showGreenBlock" @click="stopTimer">
		<span>Click Me</span>
	</div>
</template>

<script>
	export default {
		props: ['delay'],
		data() {
			return {
				showRedBlock: true,
				showGreenBlock: false,
				startTime: null,
				clickTime: null,
				earlyClick: false,
				reactionTime: 0,
			}
		},
		emits: ['end', 'impatient'],
		methods: {
			startTimer() {
				this.startTime = Date.now()
			},
			stopTimer() {
				this.clickTime = Date.now()
				this.reactionTime = ((this.clickTime - this.startTime) / 1000) * 1000
				this.$emit('end', this.reactionTime)
			},
			tooSoon() {
				this.earlyClick = true
				this.showRedBlock = false
				this.showGreenBlock = false
				this.startTime = null
				this.$emit('impatient', this.earlyClick)
			},
		},
		mounted() {
			setTimeout(() => {
				this.showRedBlock = false
				this.showGreenBlock = true
				this.startTimer()
			}, this.delay)
		},
	}
</script>

<style></style>

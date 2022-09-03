<template>
	<div>
		<button v-on:click="activateFunction">Add random actor</button>
	</div>
</template>

<script>
	export default {
		name: "Buttons",
		methods: {
			addRandom(min, max) {
				console.log(Math.floor(Math.random() * (max - min + 1) + min));
				return Math.floor(Math.random() * (max - min + 1) + min);
			},
			activateFunction() {
				const randomNumber = this.addRandom(0, this.range);
			},
		},

		props: {
			contacts: Array,
			range: Number,
		},
	};
</script>

<style></style>

<template>
	<div class="container">
		<button @click="isOpen = true">Open modal</button>
		<modal-wrap :is-open="isOpen" :title="'Main modal'" @closeModal="isOpen = false">
			<p>modal body content</p>
			<p>modal body content</p>
			<p>modal body content</p>
			<p>modal body content</p>
		</modal-wrap>
	</div>
</template>

<script>
import ModalWrap from "./components/ModalWrap.vue";

export default {
	name: "App",
	components: {
		ModalWrap,
	},

	data() {
		return {
			isOpen: false,
		};
	},

	methods: {
		openModal() {
			this.isOpen = true;
		},
	},
};
</script>

<style>
body {
	margin: 0;
	min-height: 100%;
}

#app {
	height: 100vh;
}

h1 {
	margin: 0;
}

.container {
	width: 100%;
	height: 100%;
}
</style>

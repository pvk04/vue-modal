<template>
	<div class="container">
		<button @click="isOpen = true">Open modal</button>
		<modal-wrap :is-open="isOpen" :title="'Main modal'" @closeModal="closeModal()">
			<template v-slot:body>
				<p>modal body content</p>
				<p>modal body content</p>
				<p>modal body content</p>
				<p>modal body content</p>
			</template>
			<template v-slot:footer>
				<button @click="closeModal()">ok</button>
			</template>
		</modal-wrap>
	</div>
</template>

<script>
import { sendToServer } from "./services/api.js";

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

		closeModal() {
			sendToServer();
			this.isOpen = false;
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

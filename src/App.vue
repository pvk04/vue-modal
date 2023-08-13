<template>
	<div class="container">
		<button @click="isOpen = true">Open modal</button>
		<modal-wrap
			:is-open="isOpen"
			:title="'Main modal'"
			@closeModal="
				isOpen = false;
				controlValue = '';
			"
			@confirm="confirmModal()"
		>
			<template #body>
				<p>modal body content</p>
				<p>modal body content</p>
				<p>modal body content</p>
				<p>modal body content</p>
			</template>
			<template #footer="{ confirm }">
				<input type="text" :placeholder="$options.CONFIRMATION_TEXT" v-model="controlValue" />
				<button @click="confirm" :disabled="!isConfirmationCorrect">ok</button>
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
			controlValue: "",
		};
	},

	CONFIRMATION_TEXT: "I understand",

	computed: {
		isConfirmationCorrect() {
			return this.controlValue === this.$options.CONFIRMATION_TEXT;
		},
	},

	methods: {
		openModal() {
			this.controlValue = "";
			this.isOpen = true;
		},

		confirmModal() {
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

<template>
	<div class="modal-background" :class="{ hide: !isOpen }" @click="close()">
		<div class="modal-content" @click.stop>
			<h1>{{ title }}</h1>
			<hr />
			<slot name="body">empty modal</slot>
			<hr />
			<slot name="footer" :close="close" :confirm="confirm">
				<button @click="confirm()">ok</button>
			</slot>
		</div>
	</div>
</template>

<script>
export default {
	name: "ModalWrap",
	props: {
		isOpen: {
			type: Boolean,
			required: true,
			default: false,
		},
		title: {
			type: String,
			required: true,
			default: "Modal window",
		},
	},

	emits: {
		closeModal: null,
		confirm: null,
	},

	mounted() {
		document.addEventListener("keydown", this.handleKeyDown);
	},

	beforeUnmount() {
		document.removeEventListener("keydown", this.handleKeyDown);
	},

	methods: {
		close() {
			this.$emit("closeModal");
		},

		confirm() {
			this.$emit("confirm");
		},

		handleKeyDown(event) {
			if (this.isOpen && event.key === "Escape") this.close();
		},
	},
};
</script>

<style>
.hide {
	display: none !important;
}

.modal-background {
	display: flex;
	position: fixed; /* Stay in place */
	z-index: 1; /* Sit on top */
	left: 0;
	top: 0;
	width: 100%; /* Full width */
	height: 100%; /* Full height */
	overflow: auto; /* Enable scroll if needed */
	background-color: rgb(0, 0, 0); /* Fallback color */
	background-color: rgba(0, 0, 0, 0.4); /* Black w/ opacity */
}

.modal-content {
	margin: auto;
	width: max-content;
	height: max-content;
	padding: 20px;
	background: white;
	border-radius: 5px;
}
</style>

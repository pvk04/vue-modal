<template>
	<div class="modal-background" :class="{ hide: !isOpen }" @click="close($event)">
		<div class="modal-content">
			<h1>{{ title }}</h1>
			<hr />
			<slot>empty modal</slot>
			<hr />
			<button class="closeBtn">ok</button>
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
		closeModal: true,
	},

	methods: {
		close(event) {
			console.log(event.target.classList[0] !== "modal-background" && event.target.classList[0] !== "closeBtn");
			if (event.target.classList[0] !== "modal-background" && event.target.classList[0] !== "closeBtn") return;
			this.$emit("closeModal");
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

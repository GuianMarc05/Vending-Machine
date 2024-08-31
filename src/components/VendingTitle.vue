<script setup>
defineProps({
	msg: {
		type: String,
		required: true,
	},
});
</script>

<template>
	<div class="greetings">
		<h1 class="title">{{ msg }}</h1>
		<img src="../assets/vending-machine.png" alt="Vending Machine" />
	</div>
</template>

<style scoped>
h1 {
	font-weight: 500;
	font-size: 2.6rem;
	position: relative;
	top: -10px;
}

.title {
	color: rgb(243, 245, 143);
}

h3 {
	font-size: 1.2rem;
}

.greetings {
	display: flex;
	flex-direction: column;
	align-items: center;
	justify-content: center;
}

.greetings h1,
.greetings h3 {
	display: flex;
	text-align: center;
}

@media (min-width: 1024px) {
	.greetings h1,
	.greetings h3 {
		text-align: left;
	}
}
</style>

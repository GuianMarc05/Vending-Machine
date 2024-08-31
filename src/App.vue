<script setup>
import VendingTitle from './components/VendingTitle.vue';
import VendingContent from './components/VendingContent.vue';
</script>

<template>
	<header>
		<div class="wrapper">
			<VendingTitle msg="Vending Machine" />
		</div>
	</header>

	<main>
		<VendingContent />
	</main>
</template>

<style scoped>
header {
	line-height: 1.5;
}

@media (min-width: 1024px) {
	header {
		display: flex;
		place-items: center;
		padding-right: calc(var(--section-gap) / 2);
	}

	header .wrapper {
		display: flex;
		place-items: flex-start;
		flex-wrap: wrap;
	}
}
</style>

<template>
	<div class="card">
		<slot />
	</div>
</template>

<script setup>
const { card } = defineProps(["card"]);
</script>

<style lang="scss" scoped>
.card {
	border: 1px solid #ddd;
	font-family: "Colonna MT";
	padding: 0.2cm 0.2cm 1cm;
	height: 8.8cm;
	width: 6.3cm;
}
</style>

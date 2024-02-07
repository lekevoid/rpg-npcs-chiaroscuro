<template>
	<p class="line">
		<span v-if="stats?.[stat] && stats[stat] > 0">{{ stats[stat] }}</span>
	</p>
</template>

<script setup>
const { stats, stat } = defineProps(["stats", "stat"]);
</script>

<style lang="scss" scoped>
.line {
	top: -2px;
	width: 100%;
	text-align: center;
	border-bottom: 1px solid #ddd;
}
</style>

<template>
	<div class="page" v-for="page in weapons">
		<Card v-for="weapon in page">
			<img :src="`/weapons/${weapon.img}.jpg`" class="card_img" alt="" />
			<p class="card_title">{{ weapon.name }}</p>
		</Card>
	</div>
</template>

<script setup>
function splitIntoPages(array) {
	return array.reduce((result, item, index) => {
		const chunkIndex = Math.floor(index / 8);

		if (!result[chunkIndex]) {
			result[chunkIndex] = []; // Initialize a new chunk if it doesn't exist
		}

		result[chunkIndex].push(item); // Push the current item to the chunk

		return result;
	}, []);
}

const weapons = splitIntoPages([
	{ name: "Axe", img: "axe" },
	{ name: "Bo Staff", img: "bo-staff" },
	{ name: "Bow", img: "bow" },
	{ name: "Brass Knuckles", img: "brassknuckles" },
	{ name: "Crossbow", img: "crossbow" },
	{ name: "Dagger", img: "dagger" },
	{ name: "Flashlight", img: "flashlight" },
	{ name: "Garrote", img: "garrote" },
	{ name: "Karambit", img: "karambit" },
	{ name: "Knife", img: "knife" },
	{ name: "Mace", img: "mace" },
	{ name: "Machete", img: "machete" },
	{ name: "Pepper Spray", img: "pepperspray" },
	{ name: "Pistol", img: "pistol" },
	{ name: "Baton", img: "retractablebaton" },
	{ name: "Revolver", img: "revolver" },
	{ name: "Shotgun", img: "shotgun" },
	{ name: "Shuriken", img: "shuriken" },
	{ name: "Spear", img: "spear" },
	{ name: "Steelwhip", img: "steelwhip" },
	{ name: "Sword", img: "sword" },
	{ name: "Swordcane", img: "swordcane" },
	{ name: "Taser", img: "taser" },
	{ name: "Throwingknife", img: "throwingknife" },
	{ name: "Tonfa", img: "tonfa" },
	{ name: "War club", img: "war-club" },
	{ name: "Warhammer", img: "warhammer" },
	{ name: "Whip", img: "whip" },
]);
</script>

<style lang="scss" scoped>
.page {
	box-sizing: border-box;
	height: 8.5in;
	width: 11in;
	padding: 0;
	display: flex;
	flex-flow: row wrap;
	justify-content: center;
	align-items: center;
	align-content: center;
}

.card_title {
	box-sizing: border-box;
	z-index: 10;
	position: absolute;
	bottom: 0;
	display: flex;
	justify-content: center;
	align-items: center;
	width: calc(100% - 0.6cm);
	font-size: 20px;
	font-weight: bold;
	color: #333;
	background: rgba(#fff, 0.6);
	margin: 0.1cm;
}

.card_img {
	z-index: 1;
	object-fit: contain;
	height: 100%;
	width: 100%;
	opacity: 0.6;
}
</style>

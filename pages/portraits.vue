<template>
	<header>
		<nav>
			<ul>
				<li v-for="tab in tabs" :class="[{ active: activeTab === tab.slug }]" :key="`tab_tab_${tab.slug}`">
					<button @click="activeTab = tab.slug">{{ tab.label }}</button>
				</li>
			</ul>
		</nav>
	</header>
	<nav v-for="tab in tabs" :class="['characters_restrict', { active: activeTab === tab.slug }]" :key="`characters_restrict_${tab.slug}`">
		<template v-if="allLists[tab.slug]">
			<div class="character_option" v-for="option in allLists[tab.slug]" :key="option.slug">
				<input type="checkbox" v-model="characterRestrict" :id="`option_${option.slug}`" :value="option.slug" />
				<label :for="`option_${option.slug}`">{{ option.name }}</label>
			</div>
		</template>
	</nav>
	<section v-for="tab in tabs" :class="['page', `tab_${tab.slug}`, { active: activeTab === tab.slug }]" :key="`tab_content_${tab.slug}`">
		<template v-if="allCuratedLists[tab.slug]">
			<div v-for="card in allCuratedLists[tab.slug]" class="portrait_card" :key="`char_card_${tab.slug}`">
				<img :src="`/portraits/${card.slug}.jpg`" class="portrait_img" alt="" />
			</div>
		</template>
	</section>
</template>

<script setup>
import allHumansList from "@/data/humans.json";
import allMagesList from "@/data/mages.json";
import allVampiresList from "@/data/vampires.json";
import allWerewolvesList from "@/data/werewolves.json";

const activeTab = ref("mages");
const characterRestrict = ref([]);

const tabs = [
	{ label: "Humans", slug: "humans" },
	{ label: "Mages", slug: "mages" },
	{ label: "Vampires", slug: "vampires" },
	{ label: "Werewolves", slug: "werewolves" },
];

function sortBySlug(arr) {
	arr.sort(function (a, b) {
		if (a.slug > b.slug) {
			return 1;
		}

		if (a.slug < b.slug) {
			return -1;
		}

		return 0;
	});

	return arr;
}

function slugify(str, preferredChar = "_") {
	if (!str) {
		return "";
	}

	const trimPreferredChar = new RegExp(`^${preferredChar}|${preferredChar}$`, "g");

	return str
		.normalize("NFD")
		.replace(/[\u0300-\u036f]/g, "")
		.replace(/[^\w\d]+/g, preferredChar)
		.replace(trimPreferredChar, "")
		.toLowerCase();
}

function addSlugsToList(initList) {
	return initList.map((character) => {
		const slug = slugify(character.name);
		return { ...character, slug };
	});
}

function curateCharList(initList) {
	return initList.filter((character) => {
		if (characterRestrict.value.length > 0 && !characterRestrict.value.includes(character.slug)) {
			return false;
		}
		return true;
	});
}

const allLists = computed(() => {
	return {
		humans: sortBySlug(addSlugsToList(allHumansList)),
		mages: sortBySlug(addSlugsToList(allMagesList)),
		vampires: sortBySlug(addSlugsToList(allVampiresList)),
		werewolves: sortBySlug(addSlugsToList(allWerewolvesList)),
	};
});

const allCuratedLists = computed(() => {
	return {
		humans: curateCharList(sortBySlug(addSlugsToList(allHumansList))),
		mages: curateCharList(sortBySlug(addSlugsToList(allMagesList))),
		vampires: curateCharList(sortBySlug(addSlugsToList(allVampiresList))),
		werewolves: curateCharList(sortBySlug(addSlugsToList(allWerewolvesList))),
	};
});
</script>

<style lang="scss" scoped>
@import "@/styles/header.scss";
@import "@/styles/options.scss";
@import "@/styles/print.scss";

.page {
	align-content: center;
	display: none;
	flex-flow: row wrap;
	justify-content: flex-start;
	max-width: 11in;
	min-width: 7.2in;
	padding: 1cm;
	width: 100%;

	&.active {
		display: flex;
	}
}

.portrait_img {
	align-content: center;
	display: flex;
	flex-flow: row wrap;
	justify-content: center;
	height: 8.8cm;
	width: 6.3cm;
	object-fit: cover;
	border: 1px solid #ddd;
	filter: grayscale(1);
	opacity: 0.7;

	&:nth-child(8n) {
		page-break-after: always;
	}
}
</style>

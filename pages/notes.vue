<template>
	<header>
		<nav>
			<ul>
				<li>
					<a href="/portraits">Random notes</a>
				</li>
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
		<template v-if="tab.slug === 'poisons_notes'">
			<h2>Drugs & Poisons</h2>
			<h3>Common Drugs</h3>
			<table class="picture_desc">
				<tr>
					<td class="picture"></td>
					<td class="name">Name</td>
					<td class="desc">Description</td>
				</tr>
				<tr>
					<td class="picture"></td>
					<td class="name">Cocaine</td>
					<td>
						<p>Effect : Euphoria, increased energy, alertness.</p>
						<p>Overdose: seizures, heart attack, stroke.</p>
						<p>Lethal dose: 1.2 grams.</p>
					</td>
				</tr>
				<tr>
					<td class="picture"></td>
					<td class="name">Heroin</td>
					<td>
						<p>Effect : Euphoria, pain relief, drowsiness.</p>
						<p>Overdose: slow breathing, coma, death.</p>
						<p>Lethal dose: 75-375 mg.</p>
					</td>
				</tr>
				<tr>
					<td class="picture"></td>
					<td class="name">Methamphetamine</td>
					<td>
						<p>Effect : Euphoria, increased alertness, energy.</p>
						<p>Overdose: agitation, confusion, seizures.</p>
						<p>Lethal dose: 50-100 mg.</p>
					</td>
				</tr>
				<tr>
					<td class="picture"></td>
					<td class="name">Fentanyl</td>
					<td>
						<p>Effect : Pain relief, sedation.</p>
						<p>Overdose: respiratory depression, unconsciousness, death.</p>
						<p>Lethal dose: as little as 2 mg.</p>
					</td>
				</tr>
				<tr>
					<td class="picture"></td>
					<td class="name">PCP</td>
					<td>
						<p>Effect : Euphoria, dissociation, hallucinations.</p>
						<p>Overdose: psychosis, seizures, death.</p>
						<p>Lethal dose: variable, can be as low as 5 mg.</p>
					</td>
				</tr>
				<tr>
					<td class="picture"></td>
					<td class="name">Ecstasy (MDMA)</td>
					<td>
						<p>Effect : Euphoria, increased empathy, energy.</p>
						<p>Overdose: high body temperature, dehydration, organ failure.</p>
						<p>Lethal dose: 10-20 mg/kg.</p>
					</td>
				</tr>
				<tr>
					<td class="picture"></td>
					<td class="name">Ketamine</td>
					<td>
						<p>Effect : Dissociation, hallucinations, sedation.</p>
						<p>Overdose: confusion, delirium, respiratory depression.</p>
						<p>Lethal dose: variable, around 2 grams.</p>
					</td>
				</tr>
				<tr>
					<td class="picture"></td>
					<td class="name">LSD</td>
					<td>
						<p>Effect : Hallucinations, altered perception, mood changes.</p>
						<p>Overdose: extreme agitation, psychosis, self-harm.</p>
						<p>Lethal dose: No known lethal dose.</p>
					</td>
				</tr>
				<tr>
					<td class="picture"></td>
					<td class="name">Crack Cocaine</td>
					<td>
						<p>Effect : Intense euphoria, increased energy.</p>
						<p>Overdose: cardiac arrest, seizures, stroke.</p>
						<p>Lethal dose: variable, can be as low as 500 mg.</p>
					</td>
				</tr>
				<tr>
					<td class="picture"></td>
					<td class="name">Bath Salts</td>
					<td>
						<p>Effect : Euphoria, increased energy, hallucinations.</p>
						<p>Overdose: hyperthermia, agitation, psychosis.</p>
						<p>Lethal dose: variable, can be as low as 50 mg.</p>
					</td>
				</tr>
			</table>
		</template>
		<template v-if="tab.slug === 'weapons_cards'">
			<WeaponsCards />
		</template>
	</section>
</template>

<script setup>
import allHumansList from "@/data/humans.json";
import allMagesList from "@/data/mages.json";
import allVampiresList from "@/data/vampires.json";
import allWerewolvesList from "@/data/werewolves.json";
const activeTab = ref("weapons_cards");
const characterRestrict = ref([]);

const tabs = [
	{ label: "Poisons Notes", slug: "poisons_notes" },
	{ label: "Poisons Cards", slug: "poisons_cards" },
	{ label: "Weapons", slug: "weapons_cards" },
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
@import "@/styles/cards.scss";
@import "@/styles/print.scss";

.page {
	align-content: center;
	display: none;
	flex-flow: column nowrap;
	justify-content: flex-start;
	max-width: 8.5in;
	min-width: 7.2in;
	padding: 0;
	width: 100%;

	&.active {
		display: flex;
	}
}

table.picture_desc {
	border-collapse: collapse;
	font-family: "Colonna MT";

	tr {
		border: 1px solid #ddd;
	}

	td {
		padding: 4px;
	}

	.picture {
	}

	.desc {
	}
	p {
		margin: 0;
	}
}
</style>

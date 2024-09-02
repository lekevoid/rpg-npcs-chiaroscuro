<template>
	<div class="card">
		<div class="card_side">
			<div class="prose" v-if="card.story" v-html="card.story.join('')"></div>
			<img :src="`/logos/${card.logo}.webp`" alt="" class="prose_logo" v-if="card.logo" />
		</div>
		<div class="card_side">
			<div class="field name align-baseline">
				<label><b>Name</b> :</label>
				<div class="line">
					<span v-if="card.name">{{ card.name }}</span>
				</div>
			</div>
			<div class="field desc align-baseline">
				<label><b>Desc</b> :</label>
				<div class="line">
					<span v-if="card.description">{{ card.description }}</span>
				</div>
			</div>
			<div class="stats_portrait">
				<Stats :stats="card.stats" />
				<div class="portrait">
					<img :src="`/portraits/${card.slug}.jpg`" class="portrait_img" alt="" />
					<img :src="`/logos/${card.logo}.webp`" alt="" :class="['portrait_logo', card.logo]" v-if="card.logo" />
				</div>
			</div>
			<div class="notable_tips">
				<div class="field notable_traits" v-if="card.notableTraits">
					<label><b>Notable Traits</b></label>
					<div class="trait_row" v-for="(score, trait) in card.notableTraits" :key="trait">
						<p class="line">{{ trait }}</p>
						<span class="score" v-if="score <= 5">
							<span v-for="dot in score" :key="`score_under_five_${dot}`">●</span>
						</span>
						<span class="score" v-else>
							<span class="fiveplus">◎</span>
							<span v-for="dot in score - 5" :key="`score_above_five_${dot}`">●</span>
						</span>
					</div>
				</div>
				<div class="field rp_tips" v-if="card.notableTraits">
					<label><b>Storyteller Tips</b></label>
					<p class="content" v-if="card.tips">
						<span v-for="(tip, k) in card.tips" :key="`tip_${k}`">{{ tip }}</span>
					</p>
					<p class="line" v-for="i in 13" :key="`tip_line_${i}`"></p>
				</div>
			</div>
		</div>
	</div>
</template>

<script setup>
const { card } = defineProps(["card"]);
</script>

<style lang="scss" scoped>
@import "@/styles/cards.scss";
</style>

<style lang="scss">
.prose {
	font-family: "Ink Free Regular";
	position: relative;
	z-index: 10;

	p {
		font-size: 12px;
		font-weight: 700;
		line-height: 160%;
		margin: 0 0 1em;
		text-align: justify;

		b {
			font-weight: 900;
			-webkit-text-stroke: 0.2px;
		}
	}

	h2 {
		font-size: 1.2em;
		-webkit-text-stroke: 0.2px;
		font-weight: 900;
	}

	*:first-child {
		margin-top: 0;
	}
}

.prose_logo {
	position: absolute;
	height: 80%;
	width: 80%;
	z-index: 1;
	left: 10%;
	top: 10%;
	object-fit: contain;
	opacity: 0.07;
}
</style>

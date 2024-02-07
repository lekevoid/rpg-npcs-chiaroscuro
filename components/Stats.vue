<template>
	<div class="stats">
		<section>
			<div class="icon">
				<img src="@/img/icon_physical.png" />
			</div>
			<div class="group"></div>
			<div class="stats_names">
				<p>Combat</p>
				<p>Stealth</p>
				<p>Soak</p>
				<p>Strength</p>
			</div>
			<div class="stats_scores">
				<StatsScore :stats stat="Combat" />
				<StatsScore :stats stat="Stealth" />
				<StatsScore :stats stat="Soak" />
				<StatsScore :stats stat="Strength" />
			</div>
			<div class="stats_scores_on">
				<p>/10</p>
				<p>/10</p>
				<p>/5</p>
				<p>/5</p>
			</div>
		</section>
		<section>
			<div class="icon">
				<img src="@/img/icon_social.png" />
			</div>
			<div class="group"></div>
			<div class="stats_names">
				<p>Charisma</p>
				<p>Empathy</p>
				<p>Manipulation</p>
				<p>Self-Control</p>
			</div>
			<div class="stats_scores">
				<StatsScore :stats stat="Charisma" />
				<StatsScore :stats stat="Empathy" />
				<StatsScore :stats stat="Manipulation" />
				<StatsScore :stats stat="Self-Control" />
			</div>
			<div class="stats_scores_on">
				<p>/10</p>
				<p>/10</p>
				<p>/10</p>
				<p>/5</p>
			</div>
		</section>
		<section>
			<div class="icon">
				<img src="@/img/icon_mental.png" />
			</div>
			<div class="group"></div>
			<div class="stats_names">
				<p>Alertness</p>
				<p>Culture</p>
				<p>Knowledge</p>
				<p>Willpower</p>
			</div>
			<div class="stats_scores">
				<StatsScore :stats stat="Alertness" />
				<StatsScore :stats stat="Culture" />
				<StatsScore :stats stat="Knowledge" />
				<StatsScore :stats stat="Willpower" />
			</div>
			<div class="stats_scores_on">
				<p>/10</p>
				<p>/10</p>
				<p>/10</p>
				<p>/10</p>
			</div>
		</section>
	</div>
</template>

<script setup>
const { stats } = defineProps(["stats"]);
</script>

<style lang="scss" scoped>
.stats {
	width: 152px;
}

section {
	display: flex;
	flex-flow: row nowrap;
	align-items: center;
	margin-bottom: 10px;

	.icon {
		width: 22px;
		padding-right: 2%;
	}

	.group {
		border-width: 1px;
		border-style: solid;
		border-radius: 4px 0 0 4px;
		border-color: #000 transparent #000 #000;
		height: 100%;
		min-height: 62px;
		width: 6px;
	}

	.stats_names {
		display: flex;
		flex-flow: column nowrap;
		width: 84px;
		font-family: "Ink Free Regular";
		font-weight: 700;

		p {
			font-size: 12px;
			height: 14px;
			letter-spacing: 1px;
		}
	}

	.stats_scores {
		display: flex;
		flex-flow: column nowrap;
		width: 20px;

		.line {
			top: -2px;
			width: 100%;
			text-align: center;
			border-bottom: 1px solid #ddd;
		}
	}

	.stats_scores_on {
		display: flex;
		flex-flow: column nowrap;
		width: 15px;
	}

	img {
		max-width: 100%;
	}

	p {
		margin: 0;
		line-height: 1em;
		height: 1em;
		font-size: 14px;
	}
}
</style>

<template>
	<div id="global">
		<NuxtPage />
	</div>
</template>

<style lang="scss">
body * {
	position: relative;
	box-sizing: border-box;
}

body {
	margin: 0;
	color: #111;
}

@media screen {
	#global {
		padding: 60px;
	}
}
</style>

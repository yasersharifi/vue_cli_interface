<template>
	<div class="alert selfAlert" role="alert" :class="alertClass">
		{{ alertText }}
		<button
			type="button"
			class="btn-close" @click="$emit('hide')">
		</button>
		<div class="counter">{{ alertCounter }}</div>
	</div>
</template>

<script>
export default {
	name: "Alert",
	props: ["alertClass", "alertText", "alertCounter"],
}
</script>

<style>
.selfAlert {
	position: absolute !important;
	top: 5% !important;
	right: 2% !important;
	width: auto !important;
	z-index: 1 !important;
}
.counter {
	position: absolute;
	width: 20px;
	height: 20px;
	background-color: rgb(255, 155, 0);
	border-radius: 100%;
	top: 3px;
	left: 3px;
	display: flex;
	justify-content: center;
	align-items: center;
	color: #eee;
}
</style>
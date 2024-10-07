<template>
	<div class="unkown">
		<div class="title"><i class="bi bi-exclamation-circle"></i> 未知的组件“{{data.data.name}}”</div>
		<div class="info">
			这是一个名为'{{data.data.name}}'的未知组件。
		</div>
	</div>
</template>

<script setup>
	const data = defineProps(['data'])
</script>

<style scoped>
	.title{
		font-size: 10px;
		margin-bottom: 4px;
		color: #cc900c;
	}
	.unkown{
		border: 1px solid #cc900c;
		padding: 4px;
	}
</style>
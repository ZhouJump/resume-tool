<template>
	<div class="rank-exp">
		<div v-for="rank in data.data.data" class="rank-exp-item">
			<div class="rank-title">{{rank.title}}</div>
			<div class="rank-count-box">
				<div v-for="count in rank.rank" class="rank-count"></div>
			</div>
			
		</div>
	</div>
</template>

<script setup>
	const data = defineProps(['data'])
</script>

<style>
</style>
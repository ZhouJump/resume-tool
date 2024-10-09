<template>
	<div class="fence-title">
		<i :class="['bi','icon',data.data.icon]"></i>
		<div class="title">{{data.data.title}}</div>
	</div>
</template>

<script setup>
	const data = defineProps(['data'])
</script>

<style scoped>
.fence-title{cursor: grab}
.fence-title:active{cursor: grabbing}
</style>
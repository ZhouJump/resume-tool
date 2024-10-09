<template>
	<div class="tag-list">
		<div v-for="tag in data.data.data" class="tag-item">{{tag}}</div>
	</div>
	
</template>

<script setup>
	const data = defineProps(['data'])
</script>

<style scoped>
.tag-list{cursor: grab}
.tag-list:active{cursor: grabbing}
</style>
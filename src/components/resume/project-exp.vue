<script setup>
	const data = defineProps(['data'])
</script>

<template>
	<div class="project-exp">
		<div class="title-list">
			<div v-for="title in data.data.title" class="title-item">
				{{title}}
			</div>
		</div>
		<div v-for="detail in data.data.data" class="detail">
			<div class="detail-title">{{detail.title}}</div>
			<div class="detail-text">{{detail.text}}</div>
		</div>
	</div>
</template>
    
<style scoped>
.project-exp{cursor: grab}
.project-exp:active{cursor: grabbing}
</style>
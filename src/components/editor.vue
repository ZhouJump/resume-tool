<script setup>
	import projectExp from './resume/project-exp.vue'
	import fenceTitle from "./resume/fence-title.vue"
	import rankExp from './resume/rank-exp.vue';
	import tagList from './resume/tag-list.vue';
	import unkown from './resume/unkown.vue'
	import draggable from "vuedraggable";
    const resume = defineProps(['resume'])
</script>

<template>
    <div class="resume-page">
        <div @click="$emit('chooseComp',{com:'headEdit',index:-1})" class="resume-head">
            <div class="name">{{resume.resume.head.name}}</div>
            <div class="job">{{resume.resume.head.job}}</div>
			<img class="avater" :src="resume.resume.head.avater"/>
            <div v-for="data in resume.resume.head.data" class="data">
                <div>{{data.title}}</div>
                <div>{{data.data}}</div>
				<i :class="['bi',data.icon]"></i>
            </div>
        </div>
		<draggable
			class="draggable"
			:list="resume.resume.body"
			itemKey="id"
			@start="$emit('dragstart')"
			@end="$emit('dragend')"
			fallback-class="true"
			:group="{name:'group',pull:true,put:true}">
			 <template #item="{ element,index }">
				  <div class="item">
						<project-exp @click="$emit('chooseComp',{com:'projectExpEdit',index:index})" :data="element" v-if="element.name==='projectExp'"></project-exp>
						<fence-title @click="$emit('chooseComp',{com:'fenceTitleEdit',index:index})" :data="element" v-else-if="element.name==='fenceTitle'"></fence-title>
						<rank-exp @click="$emit('chooseComp',{com:'rankExpEdit',index:index})" :data="element" v-else-if="element.name==='rankExp'"></rank-exp>
						<tag-list @click="$emit('chooseComp',{com:'tagListEdit',index:index})" :data="element" v-else-if="element.name==='tagList'"></tag-list>
						<unkown @click="$emit('chooseComp',{com:'headEdit',index:index})" :data="element" v-else></unkown>
				  </div>
			</template>
		</draggable>
    </div>
</template>
    
<style scoped>
    .resume-page{
		height: 594px;
		width: 420px;
		box-shadow: 0 0 10px rgba(0,0,0,0.1);
		transform-origin: 50% 0;
		font-size: 8px;	
	}
</style>

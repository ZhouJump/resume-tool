<template>
	<i @click="$emit('chooseComp',{com:'theme',index:0})" class="bi bi-chevron-left"></i>
	<div class="head">模块配置</div>
	<div class="title">熟练条配置</div>
	 <div v-for="(rank,i) in resume.resume.body[resume.index].data" class="other-info">
		   <input class="input" @input="resume.resume.body[resume.index].data[i].title=$event.target.value" placeholder="技术技能" :value="rank.title"/>
		   <div class="input">
				<input type="range" min="1" max="5"
					@input="resume.resume.body[resume.index].data[i].rank=$event.target.value-0"
					:value="rank.rank" style="width: 100%;"/> 
		   </div>
		   <i @click="resume.resume.body[index].data.splice(i,1)" class="bi bi-x"></i>
	  </div>
	  <div @click="resume.resume.body[index].data.push({title:'',rank:3})" class="add"><i class="bi bi-plus-lg"></i></div>
</template>

<script setup>
	const resume = defineProps(['resume','index'])
	const emit = defineEmits(["chooseComp","valueChange"])
</script>

<style scoped>
	.head{
		text-align: center;
		margin-bottom: 8px;
	}
	.title{
		color: grey;
		font-size: 12px;
		margin-bottom: 8px;
	}
	.info-cont{
		overflow: hidden;
		overflow-y: scroll;
		height: calc(100% - 210px);
	}
	.input,.input:focus{
		outline: none;
		border: 1px lightgrey solid;
		width: 100%;
		box-sizing: border-box;
		padding: 6px;
		border-radius: 6px;
		margin-bottom: 6px;
		color: #1b1b1b;
	}
	.input:hover,.input:focus{
		border-color: #2E74B5;
	}
	.other-info{
		position: relative;
	}
	.other-info .input:first-child{
		margin-bottom: 0;
		border-radius: 6px 6px 0 0;
		border-bottom: .5px dashed lightgray;
	}
	.other-info .input:nth-child(2){
		border-radius: 0 0 6px 6px;
		border-top: .5px dashed lightgray;
	}
	.other-info .input:hover,.other-info input:focus{
		border-color: #2E74B5;
	}
	.bi-chevron-left{
		position: absolute;
		cursor: pointer;
	}
	.bi-x{
		cursor: pointer;
		position: absolute;
		display: block;
		right: 4px;
		top: 4px;
		border: 1px solid lightgray;
		color: lightgray;
		width: 20px;
		line-height: 20px;
		text-align: center;
		height: 20px;
		background-color: white;
		border-radius: 16px;
	}
	.bi-x:hover{
		color: #ec4434;
		border-color: #ec4434;
	}
	.add{
		border: 1px lightgrey solid;
		width: 100%;
		box-sizing: border-box;
		padding: 4px;
		border-radius: 6px;
		text-align: center;
		color: grey;
	}
	.add:hover{
		border-color: #2E74B5;
		color: #2E74B5;
	}
</style>
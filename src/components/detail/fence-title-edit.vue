<template>
	<i @click="$emit('chooseComp',{com:'theme',index:0})" class="bi bi-chevron-left"></i>
	<div class="head">模块配置</div>
	<div class="title">标题内容</div>
	 <div class="other-info">
		   <input class="input" @input="resume.resume.body[resume.index].title=$event.target.value" placeholder="信息标题" :value="resume.resume.body[resume.index].title"/>
		   <input class="input" @input="resume.resume.body[resume.index].icon=$event.target.value" placeholder="信息图标" :value="resume.resume.body[resume.index].icon"/>
	  </div>
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
</style>
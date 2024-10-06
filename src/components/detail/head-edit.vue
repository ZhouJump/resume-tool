<script setup>
   const resume = defineProps(['resume'])
   const emit = defineEmits(["chooseComp","valueChange"])
</script>

<template>
   <i @click="$emit('chooseComp',{com:'theme',index:0})" class="bi bi-chevron-left"></i>
   <div class="head">头部配置</div>
   <div class="title">基本信息</div>
   <input @input="resume.resume.head.name=$event.target.value" placeholder="姓名" :value="resume.resume.head.name"/>
   <input @input="resume.resume.head.job=$event.target.value" placeholder="意向工作" :value="resume.resume.head.job"/>
   <div class="title">其它信息</div>
   <div class="info-cont">
	  <div class="other-info" v-for="(data,index) in resume.resume.head.data">
	  	   <input @input="resume.resume.head.data[index].title=$event.target.value" placeholder="信息标题" :value="data.title"/>
	  	   <input @input="resume.resume.head.data[index].data=$event.target.value" placeholder="信息内容" :value="data.data"/>
	  	   <input @input="resume.resume.head.data[index].icon=$event.target.value" placeholder="图标代码" :value="data.icon"/>
	  	   <i @click="resume.resume.head.data.splice(index,1)" class="bi bi-x"></i>
	  </div> 
   </div>
   <div @click="resume.resume.head.data.push({title:'',data:'',icon:''})" class="add"><i class="bi bi-plus-lg"></i></div>
</template>
    
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
		height: calc(100% - 180px);
	}
	input,input:focus{
		outline: none;
		border: 1px lightgrey solid;
		width: 100%;
		box-sizing: border-box;
		padding: 6px;
		border-radius: 6px;
		margin-bottom: 6px;
		color: #1b1b1b;
	}
	input:hover,input:focus{
		border-color: #2E74B5;
	}
	.other-info{
		position: relative;
	}
	.other-info input:first-child{
		margin-bottom: 0;
		border-radius: 6px 6px 0 0;
		border-bottom: .5px dashed lightgray;
	}
	.other-info input:nth-child(2){
		border-top: .5px dashed lightgray;
		border-bottom: .5px dashed lightgray;
		border-radius: 0;
		margin-bottom: 0;
	}
	.other-info input:nth-child(3){
		border-radius: 0 0 6px 6px;
		border-top: .5px dashed lightgray;
	}
	.other-info input:hover,.other-info input:focus{
		border-color: #2E74B5;
	}
	.bi-chevron-left{
		position: absolute;
		cursor: pointer;
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
</style>

<script setup>
	const resume = defineProps(['resume','index'])
	const emit = defineEmits(["chooseComp","valueChange"])
	import { onMounted } from 'vue';
	import { ref } from 'vue';
	
   const themeList = [
	   {name:'默认',url:'./themes/default.css',color:'#2E74B5'},
	   {name:'默认绿',url:'./themes/defaultGreen.css',color:'#0c9371'},
   ]
   const themeIndex = ref(1)
   function loadCss(url) {
		document.getElementById('theme').href=url
	}
	// onMounted(()=>{
	// 	loadCss(themeList[0].url)
	// })
</script>

<template>
   <div class="head">简历配置</div>
   <div class="title">主题配置</div>
   <div class="theme-box">
	   <div
			@click="loadCss(theme.url);themeIndex=index"
			v-for="(theme,index) in themeList"
			:style="{borderColor:theme.color,color:theme.color,borderStyle:index===themeIndex?'solid':''}"
			class="theme-item">{{theme.name}}</div>
   </div>
</template>
    
<style scoped>
    .head{
		text-align: center;
	}
	.title{
		color: grey;
		font-size: 12px;
		margin-bottom: 8px;
	}
	.theme-box{
		width: 100%;
		height: 600px;
		display: flex;
		justify-content: flex-start;
		flex-wrap: wrap;
		align-content: flex-start;
	}
	.theme-item{
		width: 90px;
		height: 120px;
		box-sizing: border-box;
		border: 4px dashed  grey;
		text-align: center;
		line-height: 60px;
		font-size: 17px;
		margin-right: 5px;
		margin-top: 5px;
	}
	.theme-item:nth-child(3n){
		margin-right: 0;
	}
</style>

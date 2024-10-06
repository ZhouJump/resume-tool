<template>
	<div style="height: 100%;">
		<input v-model="keyword" placeholder="输入以搜索,点击图标复制代码"/>
		<div class="icon-list">
			<div @click="copy('bi-'+icon)" v-for="(key,icon,index) in iconLab" v-show="icon.includes(keyword)" class="list-item">
				<i :class="['bi','bi-'+icon]"></i>
			</div>
		</div>
		<a target="_blank" href="https://icons.bootcss.com/">前往详细搜索图标</a>
	</div>
</template>

<script setup>
	import iconLab from "bootstrap-icons/font/bootstrap-icons.json"
	import { ref } from "vue";
	const keyword = ref('')
	function copy(text){
		navigator.clipboard
		  .writeText(text)
		  .then(()=>{
			  alert('代码"'+text+'"已复制,请自行粘贴使用')
		  })
	}
</script>

<style scoped>
	.icon-list{
		height: calc(100% - 96px);
		overflow: hidden;
		overflow-y: auto;
		display: flex;
		flex-wrap: wrap;
		align-content: flex-start;
	}
	.list-item{
		width: 16.6%;
		font-size: 18px;
		height: 40px;
		text-align: center;
		line-height: 40px;
		color: grey;
		border-radius: 6px;
	}
	.list-item:hover{
		background-color: #def3ff;
		color: #1262a8;
	}
	input,input:focus{
		width: 100%;
		box-sizing: border-box;
		outline: none;
		border: 1px solid lightgray;
		padding: 6px;
		border-radius: 6px;
		margin-top: 8px;
		margin-bottom: 4px;
	}
	a{
		font-size: 12px;
	}
</style>
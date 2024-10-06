<script>
	import "bootstrap-icons/font/bootstrap-icons.min.css"
    import draggable from "vuedraggable";
	import projectExp from "./components/resume/project-exp.vue";
	import fenceTitle from "./components/resume/fence-title.vue"
	import unkown from "./components/resume/unkown.vue";
	import iconLib from "./components/icon-lib.vue";
    import editor from "./components/editor.vue";
	import headEdit from "./components/detail/head-edit.vue";
	import theme from "./components/detail/theme.vue";
	export default {
	data() {
		return {
			switchIndex:0,
			pageScale:1,
			trashHide:true,
			
			trashList:[],
	
			libraryList:[
				{name:'fenceTitle',title:'项目经验',icon:'bi-briefcase-fill'},
				{name:'projectExp',title:['实习经历','2024-2025','鸡哥科技'],data:[
					{title:'工作经历:',text:'我是工作经历'},
					{title:'主要职责:',text:'我是主要职责'},
				]},
				{name:'projectExp',title:['生平履历'],data:[]},
				{name:'projectExp',title:[],data:[{title:'主要成就:',text:'我的光荣事迹'},]},
				{name:'projectExp',title:[],data:[{title:'',text:'我的光荣事迹'},]},
			],
			
			detailList:{
				component:'theme',
				index:0
			},
			
			resumeList:{
				head:{name:'张三',job:'前端开发工程师',avater:'/avater.png',data:[
					{title:'意向工作地',data:'A省B县C区',icon:'bi-geo-alt-fill'},
					{title:'电话',data:'123456789',icon:'bi-telephone-fill'},
					{title:'电邮',data:'email@email.com',icon:'bi-envelope-fill'},
				]},
				body:[
					
				],
				theme:''
			}
		}
	  },
	components: {editor,headEdit,theme,iconLib,draggable,projectExp,fenceTitle,unkown},
	methods:{
		/**指定编辑组件
		 * @param {String} component.com 组件名称
		 * @param {String} component.index 组件名称
		 */
		chooseComp(component){
			this.detailList.component = component.com
			this.detailList.index = component.index
		},
		mouseWheel(e){
			if(this.pageScale > 1 || e.wheelDeltaY>0)
				this.pageScale += e.wheelDeltaY/1200
			event.preventDefault()
		}
		
	}
	}
</script>

<template>
	<editor
		:style="{scale:pageScale}"
		@mousewheel="mouseWheel"
		@chooseComp="chooseComp"
		@dragstart="trashHide=false"
		@dragend="trashHide=true"
		class="default"
		:resume="resumeList">
		
	</editor>
    <div class="side-library box">
        <div class="switch">
			<div @click="switchIndex=0" :class="['switch-tab',switchIndex?'':'switch-active']">组件库</div>
			<div @click="switchIndex=1" :class="['switch-tab',switchIndex?'switch-active':'']">图标库</div>
		</div>
		<div v-show="!switchIndex" class="default">
			<draggable :list="libraryList" :group="{name:'group',pull:'clone',put:false}"  :sort="false">
				 <template #item="{ element }">
					  <div class="item">
							<project-exp :data="element" v-if="element.name==='projectExp'"></project-exp>
							<fence-title :data="element" v-else-if="element.name==='fenceTitle'"></fence-title>
							<unkown :data="element" v-else></unkown>
					  </div>
				</template>
			</draggable>
		</div>
		<icon-lib v-show="switchIndex"></icon-lib>
    </div>
    <div class="side-detail box">
		<component @chooseComp="chooseComp" :resume="resumeList" :is="detailList.component"></component>
    </div>
	<div :style="{bottom:trashHide?'-110px':'-20px'}" class="trach-bin box">
		<div class="trach-in">
			<draggable class="trash-drag" :list="trashList" :group="{name:'group',pull:false,put:true}" @end="trashList=[]" :sort="false">
				 <template #item="{ element }">
					  <div class="item">
							<div class="trash">
								{{element}}
							</div>
					  </div>
				</template>
			</draggable>
		</div>
		<div class="trach-face">
			<i class="bi bi-recycle"></i>
		</div>
	</div>
	<div class="head-bar box">
		
	</div>
</template>
    
<style>
    html,body,#app{
        height: 100%;
        width: 100%;
        margin: 0;
        padding: 0;
        background-color: #F7F7F7;
		cursor: default;
    }
	body{
		overflow-y: scroll;
	}
	.box{
	    padding: 10px;
	    box-sizing: border-box;
	    border-radius: 10px;
	    background-color: white;
	    box-shadow: 0 0 10px rgba(0,0,0,0.1);
	}
	.trach-bin{
		width: 260px;
		height: 110 px;
		position: fixed;
		border-radius: 24px;
		left: calc(50% - 150px);
		padding: 6px;
		background: #b5cbd9;
		box-shadow: 0 0 10px rgba(0,0,0,0.2);
	}
	.trach-bin .trach-in{
		width: 100%;
		height: 40px;
		border-radius: 16px;
		background: linear-gradient(#6a777f,#212528);
	}
	.trach-bin .trach-face{
		width: 100%;
		text-align: center;
		height: 45px;
		line-height: 45px;
		font-size: 30px;
	}
	.trash-drag{
		opacity: 0;
	}
	.head-bar{
		height: 55px;
		width: 100%;
		position: fixed;
		top:0;
		left: 0;
		border-radius: 0;
	}
	.side-library .item{
		border: 1px solid #eaeaea;
		padding: 4px;
		margin-top: 6px;
		border-radius: 6px;
	}
	.switch{
		font-size: 14px;
		display: flex;
		justify-content: space-around
	}
	.switch-tab{
		cursor: pointer;
		width: 50%;
		padding: 6px;
		box-sizing: border-box;
		text-align: center;
		color: grey;
		border: 1px solid white;
	}
	.switch-active{
		color: #2E74B5;
		border: 1px solid #2E74B5;
		border-radius: 6px;
	}
    .side-library {
        position: fixed;
        left: 10px;
        top: 70px;
        width: 300px;
        height: calc(100% - 300px);
    }
    .side-detail {
		font-size: 14px;
        position: fixed;
        right: 10px;
        top: 70px;
        width: 300px;
		height: calc(100% - 100px);
    }
	*{
		transition-duration: 200ms;
	}
</style>
<style src="./themes/default.css"></style>

<script>
	import "bootstrap-icons/font/bootstrap-icons.min.css"
	import defaultResume from "./default.json"
    import draggable from "vuedraggable";
	import domtoimage from 'dom-to-image';
	import printJS from "print-js";
	import FileSaver from "file-saver";
	import projectExp from "./components/resume/project-exp.vue";
	import fenceTitle from "./components/resume/fence-title.vue"
	import rankExp from "./components/resume/rank-exp.vue";
	import tagList from "./components/resume/tag-list.vue";
	import unkown from "./components/resume/unkown.vue";
	import iconLib from "./components/icon-lib.vue";
    import editor from "./components/editor.vue";
	import headEdit from "./components/detail/head-edit.vue";
	import projectExpEdit from "./components/detail/project-exp-edit.vue";
	import fenceTitleEdit from "./components/detail/fence-title-edit.vue";
	import rankExpEdit from "./components/detail/rank-exp-edit.vue";
	import tagListEdit from "./components/detail/tag-list-edit.vue";
	import theme from "./components/detail/theme.vue";
	export default {
	emits:['chooseComp','mousewheel','dragstart','dragend'],
	data() {
		return {
			switchIndex:0,
			pageScale:1,//简历缩放倍率
			trashHide:true,
			leftHide:false,//左侧栏隐藏状态
			rightHide:false,//右侧栏隐藏状态
			printing:false,//是否正在打印
			version:0.01,
			isFirst:localStorage.getItem('isFirst')||'1',
			
			trashList:[],
	
			libraryList:[
				{name:'fenceTitle',title:'项目经验',icon:'bi-briefcase-fill'},
				{name:'projectExp',title:['实习经历','2024-2025','鸡哥科技'],data:[
					{title:'工作经历:',text:'我是工作经历'},
					{title:'主要职责:',text:'我是主要职责'},
				]},
				{name:'projectExp',title:['生平履历'],data:[]},
				{name:'projectExp',title:[],data:[{title:'主要成就:',text:'我的光荣事迹'}]},
				{name:'projectExp',title:[],data:[{title:'',text:'我的光荣事迹'}]},
				{name:'rankExp',data:[{title:'CSS',rank:5},{title:'HTML',rank:4},{title:'JS',rank:4}]},
				{name:'tagList',data:['唱','跳','说唱','篮球','音乐']},
			],
			
			detailList:{
				component:'theme',
				index:0
			},
			
			resumeList:JSON.parse(localStorage.getItem('resume'))||defaultResume
		}
	  },
	components: {editor,headEdit,projectExpEdit,fenceTitleEdit,rankExpEdit,tagListEdit,theme,iconLib,draggable,projectExp,fenceTitle,rankExp,tagList,unkown},
	mounted() {
		setInterval(()=>{
			localStorage.setItem('resume',JSON.stringify(this.resumeList))
		},2000)
		if(this._isMobile()){
			this.leftHide=true
			this.rightHide=true
		}
		const link = document.createElement('link');
		link.rel = 'stylesheet';
		link.href = '';
		link.id = 'theme'
		document.head.appendChild(link);
		this.loadCss('./themes/defaultGreen.css')
	},
	methods:{
		/**
		 * 判断是否移动端
		 */
		_isMobile() {
		      let flag = navigator.userAgent.match(
		        /(phone|pad|pod|iPhone|iPod|ios|iPad|Android|Mobile|BlackBerry|IEMobile|MQQBrowser|JUC|Fennec|wOSBrowser|BrowserNG|WebOS|Symbian|Windows Phone)/i
		      );
		      return flag;
		},
		 loadCss(url) {
			document.getElementById('theme').href=url
		  },
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
		},
		savepic(){
			let scale = this.pageScale
			this.pageScale = 4
			this.printing = true
			setTimeout(()=>{
				domtoimage.toPng(document.getElementById('editor'))
				.then( blob => {
						this.pageScale = scale
						this.printing = false
				        FileSaver.saveAs(blob, 'resume.png');
						
				    });
			},300)
			
		},
		print(){
			let scale = this.pageScale
			this.pageScale = 4
			this.printing = true
			setTimeout(()=>{
				domtoimage.toPng(document.getElementById('editor'))
				.then( blob => {
						this.pageScale = scale
						this.printing = false
				        printJS(blob,'image')	
				    });
			},300)
			
		},
		iKnow()
		{
			localStorage.setItem('isFirst', 0)
			this.isFirst=false
		}
	}
	}
</script>

<template>
	<div id="editor" :style="{position:printing?'static':'',height:printing?'2376px':'',width:printing?'1680px':''}" class="default editor">
		<editor
			@click="rightHide=false"
			:style="{scale:pageScale,position:printing?'static':'',transformOrigin:printing?'0 0':''}"
			@mousewheel="mouseWheel"
			@chooseComp="chooseComp"
			@dragstart="trashHide=false;chooseComp({com:'theme',index:0})"
			@dragend="trashHide=true;trashList=[]"
			:resume="resumeList">
		</editor>
	</div>
	<!-- 左侧组件栏 -->
    <div :style="{left:leftHide?'-300px':''}" class="side-library box">
		<i @click="leftHide=!leftHide" :style="{rotate:leftHide?'':'180deg'}" class="bi bi-chevron-compact-right left-hide box"></i>
        <div class="switch">
			<div @click="switchIndex=0" :class="['switch-tab',switchIndex?'':'switch-active']">组件库</div>
			<div @click="switchIndex=1" :class="['switch-tab',switchIndex?'switch-active':'']">图标库</div>
		</div>
		<div v-show="!switchIndex" class="default">
			<draggable :list="libraryList" itemKey="data" :group="{name:'group',pull:'clone',put:false}"
				@start="leftHide=!leftHide" @end="leftHide=!leftHide"
				:sort="false" :clone="(e)=>{e.id=Math.random().toString(36).slice(-6);return JSON.parse(JSON.stringify(e))}">
				 <template #item="{ element }">
					  <div class="item">
							<project-exp :data="element" v-if="element.name==='projectExp'"></project-exp>
							<fence-title :data="element" v-else-if="element.name==='fenceTitle'"></fence-title>
							<rank-exp :data="element" v-else-if="element.name==='rankExp'"></rank-exp>
							<tag-list :data="element" v-else-if="element.name==='tagList'"></tag-list>
							<unkown :data="element" v-else></unkown>
					  </div>
				</template>
			</draggable>
		</div>
		<icon-lib v-show="switchIndex"></icon-lib>
    </div>
	<!-- 右侧编辑栏 -->
    <div :style="{right:rightHide?'-300px':''}" class="side-detail box">
		<i @click="rightHide=!rightHide" :style="{rotate:rightHide?'180deg':''}" class="bi bi-chevron-compact-right right-hide box"></i>
		<component @chooseComp="chooseComp" :resume="resumeList" :index="detailList.index" :is="detailList.component"></component>
    </div>
	<!-- 删除组件的垃圾桶 -->
	<div :style="{bottom:trashHide?'-110px':'-20px'}" class="trach-bin box">
		<div class="trach-in">
			<draggable class="trash-drag" :list="trashList" itemKey="id" :group="{name:'group',pull:false,put:true}" @end="trashList=[]" :sort="false">
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
	<!-- 顶栏 -->
	<div class="head-bar box">
		<div class="head-bar-left"></div>
		<div class="head-bar-right">
			<a target="_blank" href="https://blog.zhoujump.club/p/resume-tool-index/">
				<i class="bi bi-info-square"></i>
				<div>关于我</div>
				
			</a>
			<a @click="savepic">
				<i class="bi bi-download"></i>
				<div>导出图片</div>
				
			</a>
			<a @click="print">
				<i class="bi bi-printer"></i>
				<div>打印</div>
			</a>
			
		</div>
	</div>
	<!--  -->
	<div :style="{left:leftHide?'-300px':''}" class="ad box">
		AD
	</div>
	<!-- 帮助视频 -->
	<div v-if="isFirst==='1'" class="help box">
		如何使用：
		<video controls>
			<source src="../public/howtouse.mp4" type="video/mp4"/>
		</video>
		<div @click="iKnow" class="video-button">我已了解</div>
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
	div[contenteditable=true]{
		cursor: text;
	}
	.help{
		width: 50%;
		position: absolute;
		left: 25%;
		top:20%
	}
	.help video{
		width: 100%;
		border-radius: 6px;
	}
	.help .video-button{
		padding: 4px 8px 4px 8px;
		background-color: #0C9371;
		color: white;
		display: inline-block;
		text-align: center;
		border-radius: 8px;
	}
	.left-hide{
		position: absolute;
		right: -30px;
		top: 200px;
		z-index: 0;
		cursor: pointer;
		font-size: 20px;
	}
	.right-hide{
		position: absolute;
		left: -30px;
		top: 200px;
		z-index: 0;
		cursor: pointer;
		font-size: 20px;
	}
	.ad{
		position: fixed;
		z-index: 1;
		left: 10px;
		bottom: 35px;
		width: 300px;
		height: 180px;
		text-align: center;
		line-height: 160px;
		color: lightgray;
	}
	.editor {
	    height: 594px;
	    width: 420px;
	    position: relative;
	    left: calc(50% - 210px);
	    top: 80px;
	}
	.box{
	    padding: 10px;
	    box-sizing: border-box;
	    border-radius: 10px;
	    background-color: white;
	    box-shadow: 0 0 10px rgba(0,0,0,0.1);
	}
	.trach-bin{
		z-index: 2;
		width: 260px;
		height: 110px;
		position: fixed;
		border-radius: 24px;
		left: 30px;
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
		width: 100%;
		height: 100%;
	}
	.head-bar{
		height: 55px;
		width: 100%;
		position: fixed;
		top:0;
		left: 0;
		border-radius: 0;
		display: flex;
		justify-content: space-between;
	}
	.head-bar a{
		display: block;
		width: 60px;
		height: 35px;
		text-align: center;
		line-height: 20px;
		font-size: 20px;
		margin-left: 4px;
		margin-left: 4px;
		border-radius: 8px;
		color: #212528;
		text-decoration: none;
	}
	.head-bar a div{
		font-size: 10px;
	}
	.head-bar .head-bar-right{
		display: flex;
	}
	.head-bar a:hover{
		background: #eaeaea;
	}
	.side-library .item{
		border: 1px solid #eaeaea;
		padding: 4px;
		margin-top: 6px;
		border-radius: 6px;
		font-size: 8px;	
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
		z-index: 1;
    }
    .side-detail {
		font-size: 14px;
        position: fixed;
        right: 10px;
        top: 70px;
        width: 300px;
		height: calc(100% - 100px);
		z-index: 1;
    }
	*{
		transition-duration: 200ms;
	}
</style>

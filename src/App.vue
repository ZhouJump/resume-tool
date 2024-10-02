<script setup>
    import { ref } from 'vue';
    import draggable from "vuedraggable";
    import editor from "./components/editor.vue";
    const resumeList = ref({
        head:{name:'张三',job:'前端开发工程师',data:[
            {title:'意向工作地',data:'A省B县C区',icon:''},
            {title:'电话',data:'123456789',icon:''},
            {title:'电邮',data:'email@email.com',icon:''},
        ]},
        body:[],
        theme:''
    })
    const libraryList = ref([
        {name:'project-exp',theme:'default',data:{}},
        {name:'work-exp',theme:'default',data:{}}
    ])
    const detailList = ref({
       component:'theme',
       index:''
    })

</script>

<template>
    <div class="default side-library box">
        233
    </div>
    <editor class="default" :resume="resumeList">

    </editor>
    <div class="side-detail box">

    </div>
</template>
    
<style lang="scss">
    html,body,#app{
        height: 100%;
        width: 100%;
        margin: 0;
        padding: 0;
        background-color: rgb(233, 233, 233);
    }
    .box{
        padding: 10px;
        box-sizing: border-box;
        border-radius: 10px;
        background-color: white;
        box-shadow: 0 0 10px rgba(0,0,0,0.1);;
    }
    .side-library {
        position: fixed;
        left: 10px;
        top: 50px;
        width: 260px;
        height: calc(100% - 100px);
    }
    .side-detail {
        position: fixed;
        right: 10px;
        top: 50px;
        width: 260px;
    }
    .default {
        font-size: 10px;
        .resume-page {
            color:red;
        }
    }
</style>

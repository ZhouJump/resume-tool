<script setup>
    const resume = defineProps(['resume'])
</script>

<template>
    <div class="resume-page">
        <div class="resume-head">
            <div class="name">{{resume.resume.head.name}}</div>
            <div class="job">{{resume.resume.head.job}}</div>
            <div v-for="data in resume.resume.head.data" class="data">
                <div>{{data.title}}</div>
                <div>{{data.data}}</div>
                <div>{{data.icon}}</div>
            </div>
            
        </div>
    </div>
</template>
    
<style scoped>
    .resume-page {
        height: 594px;
        width: 420px;
        box-sizing: border-box;
        padding: 10px;
        background: white;
        position: relative;
        left: calc(50% - 210px);
        top: calc(50% - 297px);
        box-shadow: 0 0 10px rgba(0,0,0,0.1);
    }
</style>

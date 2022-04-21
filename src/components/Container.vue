<template>
<div>
    <div v-if="step === 0">
        <Post v-for="(posts,a) in postData" :key="a" :postData="postData[a]"/>
    </div>
    <div v-if="step === 1">
        <div :style="{backgroundImage : `url(${url})`}" class="upload-image" :class="selectedFilter"></div>
            <div class="filters">
                <FilterBox v-for="(filters,a) in filter" :key="a" :filters='filter[a]' :url='url'>
                </FilterBox>
            </div>
    </div>

    <div  v-if="step === 2">
        <div :style="{backgroundImage : `url(${url})`}" class="upload-image" :class="selectedFilter"></div>
        <div class="write">
            <textarea @change="$emit('Editcontents',content)" v-model="content" class="write-box">write!</textarea>
        </div>
    </div>

</div>
</template>

<script>
import Post from './Post.vue';
import FilterBox from './FilterBox.vue';
import filter from '../assets/filter.js';
export default {
    name: 'Container-box',
    components:{
        Post,
        FilterBox,
    },
    props : {
        postData :Array,
        step : Number,
        url : String,
    },
    data(){
        return{ 
            content : '',
            filter : filter,
            selectedFilter:''
        }
    },
    mounted(){
        this.emitter.on('selectFilter',(a)=>{
            this.selectedFilter = a
        })
    },
}
</script>

<style>
.upload-image{
width: 100%;
height: 450px;
background: cornflowerblue;
background-size : cover;
}
.filters{
overflow-x:scroll;
white-space: nowrap;
}
.filter-1 {
width: 100px;
height: 100px;
background-color: cornflowerblue;
margin: 10px 10px 10px auto;
padding: 8px;
display: inline-block;
color : white;
background-size: cover;
}
.filters::-webkit-scrollbar {
height: 5px;
}
.filters::-webkit-scrollbar-track {
background: #f1f1f1; 
}
.filters::-webkit-scrollbar-thumb {
background: #888; 
border-radius: 5px;
}
.filters::-webkit-scrollbar-thumb:hover {
background: #555; 
}
.write-box {
border: none;
width: 90%;
height: 100px;
padding: 15px;
margin: auto;
display: block;
outline: none;
}
</style>
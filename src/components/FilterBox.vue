<template>
    <div @click="fire" class="filter-item" :class="filters" :style="`background-image:url(${url})`">
    <span class="filter-name">{{filters}} </span>   
    </div>       
</template>

<script>
export default {
    name: 'Filter-Box',
    data(){
        return{
            filter : this.filters,
        }
    },
    props:{
        url :String,
        filters :String,
    },
    methods : {
        fire(){
            this.emitter.emit('selectFilter',this.filter);
        }
    },
    
}
</script>

<style>
.filter-item {
    width: 100px;
    height: 100px;
    margin: 10px 10px 10px auto;
    padding: 8px;
    display: inline-block;
    color : white;
    background-size: cover;
    background-position : center;
    position: relative;
    cursor: pointer;
}
.filter-name{
    position: absolute;
    top: 0;
    left: 1px;
    color: black;
    font-size: 0.9rem;
}
</style>
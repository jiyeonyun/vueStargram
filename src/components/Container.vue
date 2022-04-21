<template>
<div>
    <Post v-for="(posts,a) in postData" :key="a" :postData="postData[a]"/>
</div>
</template>

<script>
import Post from './Post.vue';
export default {
    name: 'Container-box',
    components:{
        Post,
    },
    props : {
        postData :Array,
    }
}
</script>

<style>

</style>
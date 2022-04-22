<template>
<div style="padding : 10px">
    <h4>팔로워</h4>
    <input @input="search($event.target.value)" placeholder="🔍" />
    <div class="post-header"  v-for="(followers,a) in follower" :key="a">
        <div class="profile" :style="{backgroundImage : `url(${followers.image})`}"></div>
        <span class="profile-name">{{followers.name}}</span>
    </div>
</div>
</template>

<script>
import {onMounted, ref} from 'vue';
import axios from 'axios';
export default {
    name: 'My-page',
    setup(){
        let follower = ref([]);
        let followerOriginal = ref([]);
            onMounted(()=>{
            axios.get('/follower.json').then((a)=>{
                        follower.value = a.data
                        followerOriginal.value = [...a.data];
                        console.log(a.data)
                    });
        });
            function search(searchd){
                let newFollowr = followerOriginal.value.filter((a)=>{
                    return a.name.indexOf(searchd) != -1
                });
                follower.value = [...newFollowr]
            }
        
        return {follower,search}
    },
    data(){
        return{
        }
    }

}

</script>

<style>

</style>
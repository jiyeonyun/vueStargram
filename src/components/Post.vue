<template>
    <div class="post">
        <div class="post-header">
        <div :style="{backgroundImage : `url(${postData.userImage})`}" class="profile"></div>
        <span class="profile-name">{{postData.name}}</span>
        </div>
        <div :style="{backgroundImage : `url(${postData.postImage})`}" class="post-body" :class="postData.filter"></div>
        <div class="post-content">
        <p>{{$store.state.postData[id].likes}} Likes</p> 
        <button v-if="hearts=== true" class="button" @click="heart">🤍</button>
        <button v-if="hearts=== false" class="button" @click="heart">❤️</button>
        <p><strong>{{postData.name}}</strong> {{postData.content}}</p>
        <p class="date">{{postData.date}}</p>
        </div>
</div> 
</template>

<script>
export default {
    name : 'post-vue',
    props : {
        postData :Array,
        id: Number,
    },
    data(){
      return{
        hearts : true,
      }
    },
    methods : {
      heart(){
        this.$store.commit('likePlus',this.id);
        this.hearts = !this.hearts;

      }
    }
}
</script>

<style>
.post {
  width: 100%;
}
.profile {
  background-image: url("https://placeimg.com/100/100/arch");
  width: 30px;
  height: 30px;
  background-size: 100%;
  border-radius: 50%;
  float: left;
}
.profile-name {
  display: block;
  float: left;
  padding-left: 10px;
  padding-top: 7px;
  font-size: 14px;
}
.post-header {
  height: 30px;
  padding: 10px;
}
.post-body {
  background-image: url("https://placeimg.com/640/480/animals");
  height: 450px;
  background-position: center;
  background-size: cover;
}
.post-content {
  padding-left: 15px;
  padding-right: 15px;
  font-size: 14px;
}
.date {
  font-size: 11px;
  color: grey;
  margin-top: -8px;
} 
.button{
  border: none;
  background: transparent;
  cursor: pointer;
  font-size: 1.3rem;
}
.button:hover{
  transform: scale(1.1);
}
</style>
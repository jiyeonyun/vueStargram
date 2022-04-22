<template>
 <div class="wrap" ref="wrap">
    <div class="header">
      <ul class="header-button-left">
        <li v-if="step>=1" @click="step--">Cancel</li>
      </ul>
      <ul class="header-button-right">
        <li v-if="step === 1" @click="step++">Next</li>
        <li v-if="step === 2" @click="publish">게시</li>
      </ul>
      <img @click="follower" src="./assets/logo.png" class="logo" />
    </div>
    <Container @Editcontents='contents = $event' :selectedFilter='selectedFilter' :postData='postData' :step='step' :url='url'/>
    <div class="footer">
      <ul class="footer-button-plus">
        <input @change="upload" accept="image/*" type="file" id="file" class="inputfile" />
        <label for="file" class="input-plus">+</label>
      </ul>
  </div>
 </div>
</template>

<script>
import Container from './components/Container.vue';
import axios from 'axios';
axios.get();
export default {
  name: 'App',
  components: {
    Container,
  },
  data(){
    return{
      postData : this.$store.state.postData,
      request : 1,
      step : 0,
      url : '',
      contents: '',
      date: new Date().toLocaleString('en-us',{month:'short', day:'numeric'}),
      tr : true,
    }
  },
  // computed:{
  // now2(){
  //     return new Date();
  //   },
  // },
  methods:{
    follower(){
      if(this.step !==3){
        this.step=3
        }
        else{
          this.step=0
          }
    },
    upload(e){
      let file = e.target.files;
      this.url = URL.createObjectURL(file[0]);
      this.step++
    },
    publish(){
      let newPost = {
        id:this.postData.length,
        name: "j1y2on",
        userImage: "https://placeimg.com/100/100/arch",
        postImage: this.url,
        likes: 0,
        date: this.date,
        liked: false,
        content: this.contents,
        filter: this.$store.state.selectedfilter,
      };
      this.postData.push(newPost);
      this.step = 0;
      this.tr = !this.tr
    },
    watch:{
    postData(){
      this.$nextTick(() => {
                let wrap = this.$ref.wrap;
                wrap.scrollTo({ top: wrap.scrollHeight, behavior: 'smooth' });
            });
    }
    }
}
}
</script>

<style>
body {
    margin: 0;
  }
  ul {
    padding: 5px;
    list-style-type: none;
  }
  .logo {
    width: 22px;
    margin: auto;
    display: block;
    position: absolute;
    left: 0;
    right: 0;
    top: 13px;
  }
  .header {
    width: 100%;
    height: 40px;
    background-color: white;
    padding-bottom: 8px;
    position: sticky;
    top: 0;
  }
  .header-button-left {
    color: skyblue;
    float: left;
    width: 50px;
    padding-left: 20px;
    cursor: pointer;
    margin-top: 10px;
  }
  .header-button-right {
    color: skyblue;
    float: right;
    width: 50px;
    cursor: pointer;
    margin-top: 10px;
  }
  .footer {
    width: 100%;
    position: sticky;
    bottom: 0;
    padding-bottom: 10px;
    background-color: white;
  }
  .footer-button-plus {
    width: 80px;
    margin: auto;
    text-align: center;
    cursor: pointer;
    font-size: 24px;
    padding-top: 12px;
  }
  .sample-box {
    width: 100%;
    height: 600px;
    background-color: bisque;
  }
  .inputfile {
    display: none;
  }
  .input-plus {
    cursor: pointer;
  }
  #app {
    box-sizing: border-box;
    font-family: "consolas";
    margin-top: 60px;
    width: 100%;
    max-width: 460px;
    margin: auto;
    position: relative;
    border-right: 1px solid #eee;
    border-left: 1px solid #eee;
  }
</style>

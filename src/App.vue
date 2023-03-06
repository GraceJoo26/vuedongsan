<template>
  <div class="menu">
    <a v-for="메뉴 in 메뉴들" :key="메뉴">{{ 메뉴 }}</a>
  </div>

  <Discount/>


  <div class="black-bg" v-if="모달창 == true">
      <div class="white-bg">
        <h3>{{ 원룸들[누른거].title }}</h3>
        <img :src=" 원룸들[누른거].image" style="width:100%;"/>
        <p>{{ 원룸들[누른거].price }}</p>
        <p>{{ 원룸들[누른거].content }}</p>
        <button @click="모달창 = false">닫기</button>
      </div>
  </div>
  <div v-for="(매물,i) in 원룸들" :key="i" >
    <img :src="원룸들[i].image" alt="" class="room-img">
    <div>
      <h3 @click="모달창=true">{{ 원룸들[i].title }}</h3>
      <p>{{ 원룸들[i].price }}</p>
      <button @click='신고수[i]++'>허위매물신고</button>
      <span>신고수: {{ 신고수[i] }}</span>
    </div>
  </div>
</template>
<script>
import data from './assets/oneroom.js';
import Discount from './Discount.vue';

export default {
  name:'App',
  data(){
    return{
      원룸들:data,
      누른거:0,
      모달창:false,
      신고수:[0,0,0,0,0,0],
      메뉴들:['Home','Store','Contact']
    }
  },
  methods:{
  },
  components:{
    Discount,
}
}
</script>

<style>
body{
  margin:0;
}
div{
  box-sizing: border-box;
}
.black-bg{
  width:100%; 
  height:100%;
  background: rgba(0,0,0,0.5);
  position:fixed;
  padding:20px;
}
.white-bg{
  width:100%;
  background: #fff;
  border-radius: 8px;
  padding:20px;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
.menu {
  background:darkslateblue;
  padding:15px; 

  border-radius: 5px;
}
.menu a{
  color:#fff;
  padding:10px;
}
.room-img{
  width:100%;
  margin-top:40px;
}
.discount{padding:10px; background-color: gray; margin:10px; border-radius: 5px;}
</style>
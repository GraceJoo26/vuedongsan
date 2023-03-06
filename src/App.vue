<template>
  <div class="menu">
    <a v-for="메뉴 in 메뉴들" :key="메뉴">{{ 메뉴 }}</a>
  </div>

  <Discount/>

  <!--자식컴포넌트가 부모가 갖고있는 데이터를 쓰려면?-->
    <!--1. props로 데이터 전송해야 함
    1)데이터 보내고
    2)등록하고
    3)쓰기
    4)v-bind = :
    -->
  <Modal :원룸들="원룸들" :누른거="누른거" :모달창="모달창"/>

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
import Modal from './Modal.vue';

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
    Modal,
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
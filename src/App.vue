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
        2. props 보낼 때 다양한 자료형 입력 가능
        1) 작명 = "문자자료"
        2) :작명= "숫자자료"
    -->
  <Modal :원룸들="원룸들" :누른거="누른거" :모달창="모달창" @closeBtn="모달창=false"/>


<!-- :작명 = 데이터[몇번째]  -->
  <Card 
  :원룸="원룸들[i]" 
  v-for="(원룸,i) in 원룸들" 
  :key="i"
  @openModal="모달창 =true; 누른거= $event"/>
  
  <!-- 
  <Card :원룸="원룸들[1]" />
  <Card :원룸="원룸들[2]" />
  <Card :원룸="원룸들[3]" />
  <Card :원룸="원룸들[4]" />
  <Card :원룸="원룸들[5]" /> -->
  
</template>
<script>
import data from './assets/oneroom.js';
import Discount from './Discount.vue';
import Modal from './Modal.vue';
import Card from './Card.vue';

export default {
  name:'App',
  data(){
    return{ 
      오브젝트:{ name:'kim',age:20},
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
    Discount:Discount,
    Modal:Modal,
    Card:Card,
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
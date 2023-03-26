<template>
  <div class="menu">
    <a v-for="메뉴 in 메뉴들" :key="메뉴">{{ 메뉴 }}</a>
  </div>

  <Discount/>
  <button @click="priceSort">가격순정렬</button>
  <button @click="sortBack">빠꾸버튼</button>

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
   <!--div class="start" :class="{end : 모달창}"-->
   <transition name="fade">
    <Modal :원룸들="원룸들" :누른거="누른거" :모달창="모달창" @closeBtn="모달창=false"/>
  </transition>
  <!--/div-->

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
      원룸들오리지널:[...data],// filter원본보존
      오브젝트:{ name:'kim',age:20},
      원룸들:data, //sort시 사용(복사본)
      누른거:0,
      모달창:false,
      신고수:[0,0,0,0,0,0],
      메뉴들:['Home','Store','Contact']
    }
  },
  methods:{
    //sort()하면 원본이 변형, map(), filter()등은 원본을 보존해줌
    sortBack(){
      this.원룸들=[...this.원룸들오리지널];
    },
    priceSort(){
      //sort
      //var array=[3,5,2];
      // array.sort(function(a,b){
      //  return a-b   ->a-b>0, a를 오른쪽, a-b<0 a를 왼쪽으로
      //  }); -> 2,3,5로 정렬됨 
      this.원룸들.sort(function(a,b){
        return a.price-b.price
      })
    }
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
.start{
  opacity:0;
  transition:all 1s;
}
.end{
  opacity:1;
  }

  /*시작시 작명-enter-from, 끝나면 enter-to*/
  .fade-enter-from{
    transform: translateY(-1000px);
  }
  .fade-enter-active{
    transition:all 1s;
  }
  .fade-enter-to{
    transform: translateY(0px);
  }
  /*퇴장애니메이션*/
  .fade-leave-from{
    transform: translateY(0px);
  }
  .fade-leave-active{
    transition:all 1s;
  }
  .fade-leave-to{
    transform: translateY(-1000px);
  }
</style>
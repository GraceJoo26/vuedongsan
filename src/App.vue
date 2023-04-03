
<!--자식컴포넌트가 부모가 갖고있는 데이터를 쓰려면?-->
    <!--1. props로 데이터 전송해야 함
    1)데이터 보내고
    2)등록하고
    3)쓰기
    -->

<!--
  모달창 디자인
  동적인 UI만드는 법:
  1. UI의 현재 상태를 데이터로 저장해둠
  2. 데이터에 따라 UI가 어떻게 보일지를 작성
-->

<!--
  =======축약해둔 컴포넌트 쓰는 법 -- 많이 안만들고 만들거만 만드는게 좋음
  1. vue 파일 import해오고
  2. 등록하고
  3. 쓰기-->
  <!--데이터바인딩은 밑에 데이터 있어야 함-->
<template>
  <div class="menu">
     <!--v-for="자유롭게작명 in 메뉴들" :key="자유롭게작명"->반복문쓸때 꼭 필요함, 반복문 돌린 요소를 컴터가 구분하기 위해 쓴다. {{ 자유롭게작명 }}-->
    <a v-for="메뉴 in 메뉴들" :key="메뉴">{{ 메뉴 }}</a>
    <!--변수 작명 2개까지 가능, (a,i) 왼쪽변수는 array내의 데이터, 오른쪽 변수는 1씩 증가하는 정수-->
  </div>

  <Discount v-if="showDiscount == true"/>
  <button @click="priceSort">낮은가격순정렬</button>
  <button @click="priceDownSort">높은가격순정렬</button>
  <button @click="sortBack">원래대로버튼</button>

  <!--
          v-on:Click = @Click
    
          쌩 js스타일: 
          1.버튼누르면 숫자 찾아서 +1해줘,
          2.그리고 +1된걸 HTML에 반영해줘
    
          vue 스타일
          실시간 렌더링으로 신고수에+1
          1.버튼 누르면 관련된 데이터만 +1,
    
          event명 정리:
          @mouseover,ctrl+space누르면 나옴
        -->
    

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
  //import {변수1, 변수2} from 경로
import data from './assets/oneroom.js';
import Discount from './Discount.vue';
import Modal from './Modal.vue';
import Card from './Card.vue';



export default {
  name:'App',
  data(){
    return{
        //data 보관함  object자료로 저장해둠 {자료이름:자료내용}
          //data 바인딩 하는 이유 
          //1) html에 하드코딩 해놓으면 나중에 변경 어려움
          //2) 실시간 렌더링 기능을 이용하려고(웹앱 사용가능 부드럽게 넘어감, 새로고침 하지 않아도 부드럽게 변경 가능) 
      showDiscount:true,
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
    
    priceDownSort(){
      this.원룸들.sort(function(a,b){
        return b.price-a.price
      })
    },
    priceSort(){

      //this는 위에 data를 지칭함. 함수안에 데이터 쓸땐 this.데이터명
      //축약해둔 컴포넌트 쓰는 법
      //1. vue파일 import해오고
      //2. components:{}에 등록하고
      //3. 쓰기


      //sort
      //var array=[3,5,2];
      // array.sort(function(a,b){
      //  return a-b   ->a-b>0, a를 오른쪽, a-b<0 a를 왼쪽으로
      //  }); -> 2,3,5로 정렬됨 
      this.원룸들.sort(function(a,b){
        return a.price-b.price
      })
    },
    sortBack(){
      this.원룸들 = [...this.원룸들오리지널];
    },
  },
  //created(){
  //서버에서 데이터 가져오는 코드~~
  //},
  /* mounted(){
    //Lifecycle Hook 걸기!
    // beforeCreate(), created(), beforeMount(), mounted(), beforeUpdate(), updated(), beforeUnmount(), unmounted()등
      setTimeout(()=>{
        //그냥함수 vs ()=>{}
        this.showDiscount = false;
      },2000);
  },
 */
//const number = document.getElementsByClassName('number');
/* mounted(){
  setInterval(()=>{
    (number -1)
  },1000);
},
 */
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

<template>
<!--데이터바인딩은 밑에 데이터 있어야 함-->
 
  
    <!--
      =======축약해둔 컴포넌트 쓰는 법 -- 많이 안만들고 만들거만 만드는게 좋음
      1. vue 파일 import해오고
      2. 등록하고
      3. 쓰기-->
    <Discount>
    
    <!--
      모달창 디자인
      동적인 UI만드는 법:
      1. UI의 현재 상태를 데이터로 저장해둠
      2. 데이터에 따라 UI가 어떻게 보일지를 작성
    -->
      <div class="black-bg" 
      v-if="모달창열렸니==true">
        <div class="white-bg">
          <h4>{{ 원룸들[누른거].title }}</h4>
          <p>{{ 원룸들[누른거].price }}원</p>
          <p>{{ 원룸들[누른거].content }}</p>
          <button @click="모달창열렸니=false">닫기</button>
        </div>
      </div>
    
      <div class="menu">
        <!--v-for="자유롭게작명 in 메뉴들" :key="자유롭게작명"->반복문쓸때 꼭 필요함, 반복문 돌린 요소를 컴터가 구분하기 위해 쓴다. {{ 자유롭게작명 }}-->
        <a v-for="a in 메뉴들" :key="a">{{ a }}</a>
    <!--변수 작명 2개까지 가능, (a,i) 왼쪽변수는 array내의 데이터, 오른쪽 변수는 1씩 증가하는 정수-->
      </div>
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
    
       <!--=======반복======--> 
       <div v-for="(원룸,i) in 원룸들" :key="i" >
        <img :src="원룸들[i].image" alt="원룸이미지" class="room-img">
        <h4 @click="모달창열렸니=true; 누른거 = i">{{ 원룸들[i].title }}</h4>
        <p>{{ 원룸들[i].price }}원</p>
        <button @click="신고수[i]++" >허위매물신고</button>
        <span> 신고수: {{ 신고수[i] }}</span>
      </div>
    </template>
    
    <script>
    import data from './assets/oneroom.js';
    //import {변수1, 변수2} from 경로
    import Discount from './Discount';
    
    export default {
      name: 'App',
      data(){
        return {
          //data 보관함  object자료로 저장해둠 {자료이름:자료내용}
          //data 바인딩 하는 이유 
          //1) html에 하드코딩 해놓으면 나중에 변경 어려움
          //2) 실시간 렌더링 기능을 이용하려고(웹앱 사용가능 부드럽게 넘어감, 새로고침 하지 않아도 부드럽게 변경 가능)
          누른거: 0,
          원룸들: data,
          모달창열렸니: false, //0,false은 닫힘, 1,true은 열림
          메뉴들: ['Home','Shop','About'],
          신고수: [0,0,0,0,0,0],
        }
      },
      methods:{
        increase(){
          this.신고수 +=1;
        }
      },//this는 위에 data를 지칭함. 함수안에 데이터 쓸땐 this.데이터명
      //축약해둔 컴포넌트 쓰는 법
      //1. vue파일 import해오고
      //2. components:{}에 등록하고
      //3. 쓰기
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
    .discount{
      background-color: #eee;
      padding:10px;
      margin:10px;
      border-radius: 5px;
    }
    </style>
    <!--자식컴포넌트가 부모가 갖고있는 데이터를 쓰려면?-->
    <!--1. props로 데이터 전송해야 함
    1)데이터 보내고
    2)등록하고
    3)쓰기
    -->
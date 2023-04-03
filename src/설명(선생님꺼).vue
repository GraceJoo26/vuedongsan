<template>

 
  
    
    
    
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
       
        <a v-for="a in 메뉴들" :key="a">{{ a }}</a>
    
      </div>
       
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
  
    import Discount from './Discount';
    
    export default {
      name: 'App',
      data(){
        return {
        
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
    .discount{
      background-color: #eee;
      padding:10px;
      margin:10px;
      border-radius: 5px;
    }
    </style>
    
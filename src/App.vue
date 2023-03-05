<template>
  <div class="menu">
    <!--v-for="자유롭게작명 in 메뉴들" :key="자유롭게작명"->반복문쓸때 꼭 필요함, 반복문 돌린 요소를 컴터가 구분하기 위해 쓴다. {{ 자유롭게작명 }}-->
    <a v-for="a in 메뉴들" :key="a">{{ a }}</a>
<!--변수 작명 2개까지 가능, (a,i) 왼쪽변수는 array내의 데이터, 오른쪽 변수는 1씩 증가하는 정수-->
  </div>
  <div v-for="(원룸상품,i) in products" :key="i">
    <h4>{{ products[i] }}</h4>
    <p >{{ price[i] }}만원</p>
    <!--두개 다 3번반복=>i를 써서 반복가능-->
  </div>
</template>

<script>

export default {
  name: 'App',
  data(){
    return {
      //data 보관함  object자료로 저장해둠 {자료이름:자료내용}
      //data 바인딩 하는 이유 
      //1) html에 하드코딩 해놓으면 나중에 변경 어려움
      //2) 실시간 렌더링 기능을 이용하려고(웹앱 사용가능 부드럽게 넘어감, 새로고침 하지 않아도 부드럽게 변경 가능)
      products:['역삼동원룸','천호동원룸','마포구원룸'],
      price:['80','70','70'],
      메뉴들:['Home','Shop','About'],
    }
  },
  components:{

  }
}
</script>

<style>
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
</style>

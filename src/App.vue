<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <div>
    <h4>{{ products[0] }}</h4>
    <p>{{ price1 }}만원</p>
  </div>
  <div>
    <h4>{{ products[1] }}</h4>
    <p>{{ price2 }}만원</p>
  </div>
  <div>
    <h4>{{ products[2] }}</h4>
    <p>{{ price2 }}만원</p>
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
      price1:80,
      price2:70,
      products:['역삼동원룸','천호동원룸','마포구원룸']
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
  margin-top: 60px;
}
</style>

<template>
  <div class="black-bg" v-if="모달창 == true">
      <div class="white-bg">
        <h3>{{ 원룸들[누른거].title }}</h3>
        <img :src=" 원룸들[누른거].image" style="width:100%;"/>
        <p>{{ 원룸들[누른거].content }}</p>
        <input v-model="month">
        <!--@input="month = $event.target.value 대신 v-model="month"-->
        <p>{{ month }}개월 선택함 : {{ 원룸들[누른거].price * month }}</p>
        <button @click="닫기버튼">닫기</button>
      </div>
  </div>
</template>

<script>
export default {
    name:'Modal_',
    data(){
      return{
        month : 1,
        date : 123,
      }
    },
    watch : {
      month(a){
        if( a >= 13){
          alert('13이상 입력하지마셈')
        } else if( a == char ){
          alert('문자사용금지')
        }
        //month라는 데이터가 변할 때 마다 여기있는 코드가 실행됨
      }   
    },
    props:{
      원룸들: Array,
      누른거: Number,
      모달창: Boolean,
    },
    methods:{
      닫기버튼() {
        this.$emit('closeBtn');
      }, 
    }
}
</script>

<style>

</style>
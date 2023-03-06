<template>
  <div class="black-bg" v-if="모달창 == true">
      <div class="white-bg">
        <h3>{{ 원룸들[누른거].title }}</h3>
        <img :src=" 원룸들[누른거].image" style="width:100%;"/>
        <p>{{ 원룸들[누른거].price }}</p>
        <p>{{ 원룸들[누른거].content }}</p>
        <!-- <button @click="모달창 = false">닫기</button> -->
      </div>
  </div>
</template>

<script>
export default {
    name:'Modal_',
    props:{
      원룸들: Array,
      누른거: Number,
      모달창: Boolean,
    }
}
</script>

<style>

</style>
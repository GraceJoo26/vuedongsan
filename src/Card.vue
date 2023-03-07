<template>
  <div>
    <img :src= "원룸.image" alt="" class="room-img">
    <div>
      <h4 @click="함수">{{ 원룸.title }}</h4>
      <p>{{ 원룸.price }}원</p>
    </div> 
  </div>
</template>

<script>

export default {
    name:'Card_',
    props: {
        원룸:Object,
    },
    methods:{
      함수(){
        this.$emit('openModal',this.원룸.id);
      },
    }
}
</script>

<style>

</style>
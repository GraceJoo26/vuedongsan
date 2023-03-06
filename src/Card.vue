<template>
  <div>
    <img :src= "원룸.image" alt="" class="room-img">
    <div>
      <p>{{ 원룸.title }}</p>
      <p>{{ 원룸.price }}원</p>
    </div>
  </div>
</template>

<script>

export default {
    name:'Card_',
    props: {
        원룸:Object,
    }
}
</script>

<style>

</style>
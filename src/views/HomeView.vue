<script setup lang="ts">
import TheWelcome from '@/components/TheWelcome.vue'
</script>

<template>

<div class="container">
  <div class="row-1">
    <div class="one">
      <img class="img-one" src="/src/assets/image.png" alt="">
    </div>
    <div class="two">
      <img class="img-two" src="/src/assets/image.png" alt="">
    </div>
  </div>
  <div class="row-2">
    <div class="three">
      <img class="img-three" src="/src/assets/image.png" alt="">
    </div>
    <div class="four">
      <img class="img-four" src="/src/assets/image.png" alt="">
    </div>
  </div>
</div>

</template>

<style>
.container {
  display: flex;
  flex-direction: column;
}

.row-1 {
  display: flex;
  background-color: darkslategrey;
  gap: 5px;
  padding: 5px 5px 0px 5px;
}

.row-2 {
  display: flex;
  background-color: darkslategrey;
  gap: 5px;
  padding: 5px;
}

.one,
.two,
.three,
.four {
  overflow: hidden;
  background-color: antiquewhite;
  width: 100px;
  height: 100px;
}

.img-one {
  display: block;
  object-fit: none;
  object-position: bottom;
}

.img-two {
  display: block;
  object-fit: none;
  object-position: -100px;
}

.img-three {
  display: block;
  object-fit: none;
  object-position: 0 -100px;
}

.img-four {
  display: block;
  object-fit: none;
  object-position: -100px -100px;
}

</style>

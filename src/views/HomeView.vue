<script setup lang="ts">
import { ref } from 'vue';
import { useBase64 } from '@vueuse/core'
import TheOutput from '../components/TheOutput.vue'

const file = ref();
const {base64: url} = useBase64(file);

const handleInput = (e: Event) => {
  file.value = (e.target as HTMLInputElement).files?.[0] || null
}
</script>

<template>
<div class="flex mt-[30px] mb-[100px]">
  <p class="mx-auto">Inspired by the work of <a href="https://www.instagram.com/traceloops" class="mx-auto inline-block" target="_blank">@traceloops</a></p>
</div>
<div class="container">
  <div v-if="!url" class="input-div m-auto">
    <input class="input" type="file" accept="image/*" @input="handleInput">
    <p v-if="!url" class="input-text">Drop an image or click to select</p>
  </div>
  <TheOutput :url="url" />
</div>

</template>

<style>
.input-div {
  width: 200px;
  height: 200px;
  background-color: #3337;
  position: relative;
  display: flex;
  overflow: hidden;
}

.output-div {
  width: 200px;
  height: 200px;
  display: flex;
}

.input {
  height: 100%;
  width: 100%;
  opacity: 0;
  position: absolute;
  z-index: 50;
  cursor: pointer;
}

.input-text {
  text-align: center;
  font-size: large;
  width: 80%;
  margin: auto;
}

.input-image {
  object-fit: cover;
  width: 100%;
  height: 100%;
}
</style>

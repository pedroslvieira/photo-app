<script setup lang="ts">
import { ref } from 'vue';
import { useBase64 } from '@vueuse/core'
import TheOutput from '../components/TheOutput.vue'

const file = ref(null)
const { base64: url } = useBase64(file)

const handleInput = (e: InputEvent) => {
  file.value = e.target.files[0]
}
</script>

<template>

<div class="container">
  <div class="input-div">
    <input class="input" type="file" accept="image/*" @input="handleInput">
    <img v-if="url" class="input-image" :src="url" alt="" />
    <p v-if="!url" class="input-text">Drop an image or click to select</p>
  </div>
  <div v-if="!url" class="output-div">
    <p class="input-text">No image selected</p>
  </div>
  <TheOutput :url="url" />
</div>

</template>

<style>
.container {
  display: flex;
  gap: 40px;
}


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
  border: dotted 3px #3339;
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

<template>
<div class="output">
    <img class="input-image" :src="url" alt="" />
</div>
</template>

<style>
.output {
    width: 200px;
    height: 200px;
}
</style>

<script setup lang="ts">
defineProps({
    url: String
})
</script>
<template>
<img class="output-image" src="../assets/image.png" alt="" id="image" />
<div class="output">
    <canvas id="canvas"></canvas>
</div>
</template>

<style>
.output-image {
    width: 200px;
    height: 200px;
}

#canvas {
    height: 400px;
    width: 400px;
}
</style>

<script setup lang="ts">
import { onMounted } from 'vue';

const props = defineProps({
    url: String
})

const canvas = document.getElementById('canvas') as HTMLCanvasElement | null
const image = document.getElementById('image') as HTMLImageElement

const square = 25;
const coords: [number, number][] = [];
const pieces = [0, 1, 2, 3, 4, 5, 6, 7]
pieces.forEach((piece) => {
    coords.push([piece, 0], [piece, 1], [piece, 2], [piece, 3], [piece, 4], [piece, 5], [piece, 6], [piece, 7])
})

const draw = () => {
    const ctx = canvas?.getContext("2d");
    
    let coordX = 0;
    let coordY = 0;
    
    coords.forEach((coord) => {
        coordX = coord[0];
        coordY = coord[1];
        ctx?.drawImage(image, coordX*square, coordY*square, square, square, 2*coordX*square, 2*coordY*square, square, square);
        ctx?.drawImage(image, coordX*square, coordY*square, square, square, 2*coordX*square + square, 2*coordY*square, square, square);
        ctx?.drawImage(image, coordX*square, coordY*square, square, square, 2*coordX*square + square, 2*coordY*square + square, square, square);
        ctx?.drawImage(image, coordX*square, coordY*square, square, square, 2*coordX*square, 2*coordY*square + square, square, square);
    });
}
onMounted(() => {
    draw()
})
</script>
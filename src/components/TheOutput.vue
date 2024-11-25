<template>
    <div v-if="!drew && url" class="w-[200px] h-[200px] flex flex-col gap-4 items-center m-auto">
        <img class="output-image bg-contain" :src="url" alt="" id="image" />
        <button class="bg-black px-4 py-2 rounded-full" @click="draw()">Generate</button>
    </div>
    <div class="output flex flex-col gap-4 items-center m-auto">
        <canvas width="400" height="400" class="hidden" id="canvas"></canvas>
        <button v-if="drew" class="bg-black px-4 py-2 rounded-full" @click="downloadImage()">Download</button>
    </div>
</template>

<script setup lang="ts">
import { defineProps, ref } from 'vue'
defineProps({
    url: String
})

const drew = ref(false)

let square = 25;
const coords: [number, number][] = [];
const pieces = [0, 1, 2, 3, 4, 5, 6, 7]
pieces.forEach((piece) => {
    coords.push([piece, 0], [piece, 1], [piece, 2], [piece, 3], [piece, 4], [piece, 5], [piece, 6], [piece, 7])
})

const draw = () => {
    drew.value = true;

    const canvas = document.getElementById('canvas') as HTMLCanvasElement;
    const image = document.getElementById('image') as HTMLImageElement;

    const offScreenCanvas = document.createElement('canvas');
    offScreenCanvas.width = 200;
    offScreenCanvas.height = 200;
    const offScreenCtx = offScreenCanvas.getContext('2d');

    const imgWidth = image.naturalWidth;
    const imgHeight = image.naturalHeight;
    const squareSize = Math.min(imgWidth, imgHeight);

    // Calculate the starting coordinates for clipping from the center
    const startX = (imgWidth / 2) - (squareSize / 2);
    const startY = (imgHeight / 2) - (squareSize / 2);

    // Draw the resized image onto the off-screen canvas
    offScreenCtx?.drawImage(image, startX, startY, squareSize, squareSize, 0, 0, 200, 200);
    
    const ctx = canvas.getContext("2d");
    
    let coordX = 0;
    let coordY = 0;
    
    canvas.classList.remove('hidden');
    coords.forEach((coord) => {
        coordX = coord[0];
        coordY = coord[1];
        ctx?.drawImage(offScreenCanvas, coordX*square, coordY*square, square, square, 2*coordX*square, 2*coordY*square, square, square);
        ctx?.drawImage(offScreenCanvas, coordX*square, coordY*square, square, square, 2*coordX*square + square, 2*coordY*square, square, square);
        ctx?.drawImage(offScreenCanvas, coordX*square, coordY*square, square, square, 2*coordX*square + square, 2*coordY*square + square, square, square);
        ctx?.drawImage(offScreenCanvas, coordX*square, coordY*square, square, square, 2*coordX*square, 2*coordY*square + square, square, square);
    });
}

const downloadImage = () => {
    const canvas = document.getElementById('canvas') as HTMLCanvasElement;
    const link = document.createElement('a');
    link.href = canvas.toDataURL('image/png');
    link.download = 'canvas-image.png';
    link.click();
}

</script>
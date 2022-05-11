<template>
<div class="container">
    <div id="cube" :style="{transform: `rotateX(${xRotateValue}deg) rotateY(${yRotateValue}deg)`}">
        <div class="front">
            <span class="dot middle"></span>
        </div>
        <div class="back">
            <span class="dot topLeft"></span>
            <span class="dot topRight"></span>
            <span class="dot middleLeft"></span>
            <span class="dot middleRight"></span>
            <span class="dot bottomLeft"></span>
            <span class="dot bottomRight"></span>
        </div>
        <div class="right">
            <span class="dot topLeft"></span>
            <span class="dot topRight"></span>
            <span class="dot middle"></span>
            <span class="dot bottomLeft"></span>
            <span class="dot bottomRight"></span>
        </div>
        <div class="left">
            <span class="dot topLeft"></span>
            <span class="dot bottomRight"></span>
        </div>
        <div class="top">
            <span class="dot topLeft"></span>
            <span class="dot topRight"></span>
            <span class="dot bottomLeft"></span>
            <span class="dot bottomRight"></span>
        </div>
        <div class="bottom">
            <span class="dot topLeft"></span>
            <span class="dot middle"></span>
            <span class="dot bottomRight"></span>
        </div>
    </div>
    </div>
</template>

<script setup lang="ts">
import {ref, toRefs, watchEffect } from 'vue'
const props = defineProps({
    colour: {
        type: String,
        default: 'rgba(200, 0, 0, 0.9)'
    },
    dotColour: {
        type: String,
        default: '#ffffff'
    },
    rollValue: {
        type: Number,
        default: 1,
        validator: (value: number) => value >= 1 && value <= 6
    },
})

const {colour, dotColour, rollValue} = toRefs(props)

const xRotateValue = ref(0),
    yRotateValue = ref(0)
watchEffect(() => {
    let xRotation = 0,
        yRotation = 0
    switch(rollValue.value) {
        case 1:
            xRotation = 0
            yRotation = 0
            break;
        case 2:
            xRotation = 0
            yRotation = 90
            break
        case 3:
            xRotation = 90
            yRotation = 0
            break
        case 4:
            xRotation = -90
            yRotation = 0
            break
        case 5:
            xRotation = 0
            yRotation = -90
            break
        case 6:
            xRotation = 0
            yRotation = 180
            break
        default:
            break
    }

    const randomiseSpin = () => Math.floor(Math.random() * 10 - 5) * 360

    xRotateValue.value = xRotation + randomiseSpin()
    yRotateValue.value = yRotation + randomiseSpin()
})
</script>

<style scoped>

#cube {
    width: 100%;
    height: 100%;
    position: absolute;
    transform-style: preserve-3d;
    transition: transform 6s;
}
.front {
    transform:
    translateZ(100px);
}

.back {
    transform:
    rotateX(-180deg)
    translateZ(100px);
}

.right {
    transform:
    rotateY(90deg)
    translateZ(100px);
}

.left {
    transform:
    rotateY(-90deg)
    translateZ(100px);
}

.top {
    transform:
    rotateX(90deg)
    translateZ(100px);
}

.bottom {
    transform:
    rotateX(-90deg)
    translateZ(100px);
}

.front, .back, .left, .right, .top, .bottom {
    background-color: v-bind(colour);
    width: 100%;
    height: 100%;
    border:#ab1a1a solid 2px;
    display: block;
    position: absolute;
    margin: 0 auto;
    box-shadow: 0 0 3em #0006 inset;
}

.container {
    width: 200px;
    height: 200px;
    position: relative;
    margin: 0 auto 40px;
    perspective: 1000px;
    perspective-origin: 50% 50%;
}

.dot {
    display: block;
    position: absolute;
    width: 30px;
    height: 30px;
    background-color: v-bind(dotColour);
    border-radius: 50%;
}

.dot.middle {
    top: 85px;
    left: 85px;
}

.dot.topLeft {
    top: 45px;
    left: 45px;
}

.dot.topRight {
    top: 45px;
    left: 125px;
}

.dot.middleLeft {
    top: 85px;
    left: 45px;
}

.dot.middleRight {
    top: 85px;
    left: 125px;
}

.dot.bottomLeft {
    top: 125px;
    left: 45px;
}

.dot.bottomRight {
    top: 125px;
    left: 125px;
}
</style>
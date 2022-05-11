<template>
<div class="roller-container">
    <Dice :roll-value="rollValue"></Dice>
    <div class="message-display">{{message}}</div>
    <a href="#" class="roll-button" @click="onRollClicked">Let's Roll!</a>
</div>
    
</template>

<script setup lang="ts">
import Dice from './Dice.vue';
import { nextTick, ref } from 'vue';
const rollValue = ref(1)
const message = ref('Click button to roll!')
let timeout: number | undefined = undefined
const onRollClicked = () => {
    rollValue.value = rollValue.value === 6 ? 1 : rollValue.value + 1 // Set a different value to force a roll
    nextTick(() => rollValue.value = Math.floor(Math.random() * 6) + 1)
    message.value = 'Rolling!'
    if(timeout !== undefined) {
        clearTimeout(timeout)
        timeout = undefined;
    }
    timeout = setTimeout(() => {
        message.value = `You rolled a ${rollValue.value}!`
    }, 6000)
}
</script>

<style scoped>
.roller-container {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    height: 100vh;
}

.title {
    padding-bottom: 1em;
}

.message-display {
    padding: 2em;
}

.roll-button {
    font-weight: bold;
    min-width: 8em;
    color: #37474f;
    background-color: white;
    font-size: 1rem;
    text-decoration: none;
    padding: 1em 2em;
    border: 2px solid #37474f;
    border-radius: 2em;
    transition: all 400ms linear;
}

.roll-button:hover {
    color: white;
    background: #37474f;
}
</style>
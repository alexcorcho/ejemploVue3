<script setup>
import { ref } from 'vue';
const cunter = ref(0);
const increment = () => cunter.value++
</script>

<template>
    <button @click="increment">Counter {{ cunter }}</button>
</template>
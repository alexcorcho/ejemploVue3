<script setup>
// const emit = defineEmits(['next','pref'])
defineProps(["inicio", "fin", "maxLength"])
</script>

<template>
    <div class="btn-group" role="group" aria-label="Basic example">
        <button
         @click="$emit('pref')"
         type="button"
         class="btn btn-primary"
         :disabled="inicio <= 0">
         Atras {{ inicio }}
        </button>
        <button @click="$emit('next')" type="button" class="btn btn-primary" :disabled="fin >= maxLength">Adelante {{ fin }}</button>
    </div>
</template>
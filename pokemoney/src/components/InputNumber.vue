<script setup lang="ts">
import { ref } from 'vue'
const emit = defineEmits(['submitnum'])

const amount = ref(0)

function submit() {
    emit('submitnum', amount)
}
</script>

<template>
    <div class="overlay">
        <div class="modal">
            <input type="number" v-model="amount"/>
            <button @click="submit">Submit</button>
        </div>
    </div>
</template>
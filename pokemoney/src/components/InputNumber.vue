<script setup lang="ts">
import { ref } from 'vue'
const emit = defineEmits(['submitnum','close'])

const amount = ref()

function submit() {
    if (amount.value==0 || isNaN(amount.value)) {
        emit('close')
    } else {
        emit('submitnum', amount.value)
    }
}
</script>

<template>
    <div class="overlay" @click.self="emit('close')">
        <div class="modal">
            <input type="number" v-model="amount"/>
            <button @click="submit">Submit</button>
        </div>
    </div>
</template>
<style scoped>
.overlay {
    position: fixed;
    z-index: 1;
    background-color: #00000055;
    height: 100vh;
    width: 100%;
    inset: 0;
    display: flex;
    justify-content: center;
    align-items: center;
}
.modal{
    padding: 3rem;
    background-color: black;
}

</style>
<script setup lang="ts">
import InputNumber from '@/components/InputNumber.vue';
import { ref } from 'vue'

const count = ref(0)
const isModalOpen = ref(false)

function reflect(num: number) {
    isModalOpen.value = false
    count.value = num
}

</script>

<template>
<h1>{{ count }}</h1>
<InputNumber v-if="isModalOpen" @submitnum="(num) => reflect(num)" />
<button type="button" @click="isModalOpen=true">Count up</button>
</template>
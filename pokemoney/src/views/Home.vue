<script setup lang="ts">
import { ref } from 'vue'

const count = ref(0)
</script>

<template>
<h1>{{ count }}</h1>
<button type="button" @click="count++">Count up</button>
</template>
<script setup lang="ts">

defineProps<{ label: string, amount: number }>()
</script>

<template>
<div>
    <h4>{{ label }}</h4>
    <span>{{ amount }}</span>
</div>
</template>
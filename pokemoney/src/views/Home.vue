<script setup lang="ts">
import InputNumber from '@/components/InputNumber.vue'
import ShowAmount from '@/components/ShowAmount.vue'
import { ref } from 'vue'

const isModalOpen = ref(false)
const flowData = [
    {id: 1, name: "flow1", from: 0, to: 1, direction: "↓"},
    {id: 2, name: "flow2", from: 0, to: 3, direction: "↓"},
    {id: 3, name: "flow3", from: 1, to: 2, direction: "→"},
    {id: 4, name: "flow4", from: 2, to: 1, direction: "←"},
    {id: 5, name: "flow5", from: 1, to: 4, direction: "↓"},
    {id: 6, name: "flow6", from: 2, to: 4, direction: "↓"},
    {id: 7, name: "flow7", from: 3, to: 5, direction: "↓"}
]
const labelData = [
    {id: 1, name: "div1", label: "貯金箱"},
    {id: 2, name: "div2", label: "財布"},
    {id: 3, name: "div3", label: "財布"},
    {id: 4, name: "div4", label: "支出"},
    {id: 5, name: "div5", label: "経費"}
]

const saveData = localStorage.getItem("amount")
const amount = ref(saveData ? JSON.parse(saveData) : [0, 0, 0, 0, 0, 0])
const nextFlow = ref(0)

function reflect(num: number) {
    isModalOpen.value = false
    const flow = flowData.find((flow) => flow.id === nextFlow.value)
    if (flow) {
        amount.value[flow.from] -= num
        amount.value[flow.to] += num
    }
    localStorage.setItem('amount', JSON.stringify(amount.value))
}
function openModal(flowNum: number) {
    isModalOpen.value = true
    nextFlow.value = flowNum

}

</script>

<template>
<InputNumber v-if="isModalOpen" @submitnum="(num) => reflect(num)" @close="isModalOpen=false"/>
<div class="parent">
    <button 
        type="button"
        v-for="flow in flowData"
        :class="flow.name"
        @click="openModal(flow.id)"
    >
        {{ flow.direction }}
    </button>
    <ShowAmount
        v-for="label in labelData"
        :class="label.name"
        :label="label.label"
        :amount="amount[label.id]"
    />
</div>
</template>

<style>
.parent { 
display: grid; 
grid-template-columns: repeat(3, 1fr); 
grid-template-rows: 1fr 0.5fr 1fr 0.5fr repeat(2, 1fr); 
grid-column-gap: 0px;
grid-row-gap: 0px; 
}
.flow1 { grid-area: 1 / 1 / 2 / 2; } 
.flow2 { grid-area: 1 / 3 / 2 / 4; } 
.flow3 { grid-area: 2 / 1 / 3 / 3; } 
.div1 { grid-area: 3 / 1 / 4 / 2; } 
.div2 { grid-area: 3 / 2 / 4 / 3; } 
.div3 { grid-area: 3 / 3 / 4 / 4; } 
.flow4 { grid-area: 4 / 1 / 5 / 3; } 
.flow5 { grid-area: 5 / 1 / 6 / 2; } 
.flow6 { grid-area: 5 / 2 / 6 / 3; } 
.flow7 { grid-area: 5 / 3 / 6 / 4; } 
.div4 { grid-area: 6 / 1 / 7 / 3; } 
.div5 { grid-area: 6 / 3 / 7 / 4; } 
</style>
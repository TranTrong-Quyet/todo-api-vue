<script setup>
import { defineProps } from 'vue';

const props = defineProps({
    bg: {
        type: String,
        default: 'bg-gray-300'
    }
})

</script>

<template>
    <div v-bind:class="`${bg} p-8 rounded-md`">
        <slot></slot>
    </div>
</template>
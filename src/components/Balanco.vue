<script setup>
    import { defineProps } from 'vue';
    
    const props = defineProps({
        total: {
            type: Number,
            required: true,
        }
    })
</script>

<template>
    <h4>Seu Balanço</h4>
    <h1 id="balanco">R${{ total }}</h1>
</template>

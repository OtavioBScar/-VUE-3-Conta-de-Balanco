<script setup>
    import { defineProps } from 'vue';

    const props = defineProps({
        renda: {
            type: Number,
            required: true,
        },
        despesa: {
            type: Number,
            required: true,
        }
    })
</script>

<template>
    <div class="des-ren-container">
        <div class="title">
            <h4>Renda</h4>
            <p id="dinheiro-plus" class="dinheiro plus">R${{ renda }}</p>
        </div>
        <div class="title">
            <h4>Despesa</h4>
            <p id="dinheiro-minus" class="dinheiro minus">R${{ despesa }}</p>
        </div>
    </div>
</template>
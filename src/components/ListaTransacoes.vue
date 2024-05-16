<script setup>
import { defineProps } from 'vue';

const props = defineProps({
    transacoes: {
        type: Array,
        required: true,
    },
});
</script>

<template>
    <h3>Histórico</h3>
    <ul id="lista" class="lista">
        <li v-for="transacao in transacoes" :key="transacao.id" :class="transacao.quantidade < 0 ? 'minus' : 'plus'">
            {{ transacao.texto }} <span>{{ transacao.quantidade }}</span>
            <button class='delete-btn'>x</button>
        </li>
    </ul>
</template>
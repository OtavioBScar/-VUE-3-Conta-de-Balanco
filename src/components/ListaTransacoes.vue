<script setup>
import { defineProps } from 'vue';

const emitir = defineEmits(['transacaoDeletada'])

const props = defineProps({
    transacoes: {
        type: Array,
        required: true,
    },
});

const deleteTransaction = (id) => {
    emitir('transacaoDeletada', id)
}
</script>

<template>
    <h3 class="title">Histórico</h3>
    <ul id="lista" class="lista">
        <li class="title" v-for="transacao in transacoes" :key="transacao.id" :class="transacao.preco < 0 ? 'minus' : 'plus'">
            {{ transacao.texto }} <span>{{ transacao.preco }}</span>
            <button class='delete-btn' @click="deleteTransaction(transacao.id)">x</button>
        </li>
    </ul>
</template>
<script setup>
import Balanco from './components/Balanco.vue';
import Cabecalho from './components/Cabecalho.vue';
import DespesasRenda from './components/DespesasRenda.vue'
import ListaTransacoes from './components/ListaTransacoes.vue';
import AdicionarTransacao from './components/AdicionarTransacao.vue';
import { ref } from 'vue'//Função para deixar a lista reativa

const transacoes = ref([
  { id: 1, texto: "Flores", quantidade: -23.99 },
  { id: 2, texto: "Salario", quantidade: 1442.87 },
  { id: 3, texto: "Caneca", quantidade: -14.55 },
]);
</script>

<template>
  <Cabecalho />
  <div class="container">
    <Balanco />
    <DespesasRenda />
    <ListaTransacoes :transacoes="transacoes" />
    <AdicionarTransacao />
  </div>
</template>

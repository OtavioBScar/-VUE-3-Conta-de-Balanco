<script setup>
import Balanco from './components/Balanco.vue';
import Cabecalho from './components/Cabecalho.vue';
import DespesasRenda from './components/DespesasRenda.vue'
import ListaTransacoes from './components/ListaTransacoes.vue';
import AdicionarTransacao from './components/AdicionarTransacao.vue';
import { ref, computed } from 'vue'//Função para deixar a lista reativa
import { useToast } from 'vue-toastification';

const toast = useToast();

const transacoes = ref([
  { id: 1, texto: "Flores", preco: -23.99 },
  { id: 2, texto: "Salario", preco: 1442.87 },
  { id: 3, texto: "Caneca", preco: -14.55 },
]);

// Calcula o total
const total = computed(() => {
  return transacoes.value.reduce((acumulador, transacao) => {
    return acumulador + transacao.preco;
  }, 0);
});

//Calcula Renda
const renda = computed(() => {
  return transacoes.value
    .filter((transacao) => transacao.preco > 0)
    .reduce((acumulador, transacao) => {
      return acumulador + transacao.preco;
    }, 0).toFixed(2);
});

//Calcula despesa
const despesa = computed(() => {
  return transacoes.value
    .filter((transacao) => transacao.preco < 0)
    .reduce((acumulador, transacao) => {
      return acumulador + transacao.preco;
    }, 0).toFixed(2);
});

//add transaction
const HandleTransactionSubmitted = (dadosTransacao) => {
  transacoes.value.push({
    id: generateId(),
    texto: dadosTransacao.text,
    preco: dadosTransacao.quantidade
  })
  
  toast.success("transação adicionada")
}

const generateId = () => {
  return Math.floor(Math.random() * 1000000);
}

</script>

<template>
  <Cabecalho />
  <div class="container">
    <Balanco :total="+total" />
    <DespesasRenda :renda="+renda" :despesa="+despesa" />
    <ListaTransacoes :transacoes="transacoes" />
    <AdicionarTransacao @transacoessubmit="HandleTransactionSubmitted"/>
  </div>
</template>

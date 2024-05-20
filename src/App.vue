<script setup>
import Balanco from './components/Balanco.vue';
import Cabecalho from './components/Cabecalho.vue';
import DespesasRenda from './components/DespesasRenda.vue'
import ListaTransacoes from './components/ListaTransacoes.vue';
import AdicionarTransacao from './components/AdicionarTransacao.vue';
import { ref, computed, onMounted } from 'vue'//Função para deixar a lista reativa
import { useToast } from 'vue-toastification';

const toast = useToast();

const transacoes = ref([]);

onMounted(() => {
  const transacoesSalvas = JSON.parse(localStorage.getItem('transacoes'));

  if (transacoesSalvas) {
    transacoes.value = transacoesSalvas;
  }
});

// Calcula o total
const total = computed(() => {
  return transacoes.value.reduce((acumulador, transacao) => {
    return acumulador + transacao.preco;
  }, 0).toFixed(2);
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

  salvarTransacoesnoLocalStorage();

  toast.success("transação adicionada")
}

const generateId = () => {
  return Math.floor(Math.random() * 1000000);
}

const handleTransacaoDeletada = (id) => {
  transacoes.value = transacoes.value.filter((transacao) => transacao.id !== id);

  salvarTransacoesnoLocalStorage();

  toast.success("transação deletada")
}

// Salvar no localStorage
const salvarTransacoesnoLocalStorage = () => {
  localStorage.setItem('transacoes', JSON.stringify(transacoes.value))
}
</script>

<template>
  <div class="container">
    <div class="minicont">
      <Cabecalho />
      <Balanco :total="+total" />
      <DespesasRenda :renda="+renda" :despesa="+despesa" />
      <ListaTransacoes :transacoes="transacoes" @transacaoDeletada="handleTransacaoDeletada" />
      <AdicionarTransacao @transacoessubmit="HandleTransactionSubmitted" @maismenos="HandleMaisMenos" />
    </div>
  </div>
</template>

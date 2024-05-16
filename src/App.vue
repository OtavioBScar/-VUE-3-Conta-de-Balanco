<script>
  import Balanco from './components/Balanco.vue';
  import Cabecalho from './components/Cabecalho.vue';
  import DespesasRenda from './components/DespesasRenda.vue'
  import ListaTransacoes from './components/ListaTransacoes.vue';
  import AdicionarTransacao from './components/AdicionarTransacao.vue';

  export default {
    components: {
      Cabecalho,
      Balanco,
      DespesasRenda,
      ListaTransacoes,
      AdicionarTransacao,
    },
  }
</script>

<template>
  <Cabecalho />
  <div class="container">
    <Balanco />
    <DespesasRenda />
    <ListaTransacoes />
    <AdicionarTransacao />
  </div>
</template>


<script setup>
    import { ref } from 'vue';
    import { useToast } from 'vue-toastification'

    const toast = useToast();

    const text = ref('')
    const quantidade = ref('')

    const emitir = defineEmits(['transacoessubmit'])

    const onSubmit = () => {
        if(!text.value || !quantidade.value){
            toast.error('Preencha as duas caixas');
            return;
        }
        const dadosTransacao = {
            text: text.value,
            quantidade: parseFloat(quantidade.value)
        }

        emitir('transacoessubmit', dadosTransacao)

        text.value = '';
        quantidade.value = '';
    }
</script>

<template>
    <h3>Adicionar nova transação</h3>
    <form id="form" @submit.prevent="onSubmit">
        <div class="form-control">
            <label for="text">Texto</label>
            <input type="text" id="text" v-model="text" placeholder="Adicione texto..." />
        </div>
        <div class="form-control">
            <label for="quantidade">
                Preço <br/>
                ( valor = Renda, -valor = despesa)
            </label>
            <input type="text" id="quantidade" v-model="quantidade"  placeholder="Adicione quantidade..." />
        </div>
        <button class="btn">Adicionar transação</button>
    </form>
</template>

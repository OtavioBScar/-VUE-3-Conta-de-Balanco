<script setup>
import { useToggle } from '@vueuse/core';
import { ref } from 'vue';
import { useToast } from 'vue-toastification'

const toast = useToast();

const text = ref('')
const quantidade = ref('')

const emitir = defineEmits(['transacoessubmit'])

const checkvalue = {
    valor: [],
}

const mostracheck = () => {
    if (checkvalue.valor.length > 0) {
        checkvalue.valor = []
    }
}

const onSubmit = () => {
    if (!text.value || !quantidade.value) {
        toast.error('Preencha as duas caixas');
        return;
    }
    if (checkvalue.valor.length <= 0){
        quantidade.value = parseFloat(-quantidade.value)
    } else {
        quantidade.value = parseFloat(quantidade.value)
    }
    let quantity = quantidade.value
    const dadosTransacao = {
        text: text.value,
        quantidade: quantity
    }

    emitir('transacoessubmit', dadosTransacao)

    text.value = '';
    quantidade.value = '';
}

</script>

<template>
    <h3 class="title">Adicionar nova transação</h3>
    <form id="form" @submit.prevent="onSubmit">
        <div class="form-control">
            <label class="title" for="text">Texto</label>
            <input type="text" id="text" v-model="text" placeholder="Adicione texto..." />
        </div>
        <div class="form-control">
            <label class="title" for="quantidade">
                Preço <br />
                <label class="switch">
                    <input type="checkbox" value="checkado" v-model="checkvalue.valor" @click="mostracheck">
                    <input type="text" id="quantidade" v-model="quantidade" placeholder="Adicione quantidade..." />
                </label>
            </label>
        </div>
        <button class="btn">Adicionar transação</button>
    </form>
</template>

<style scoped>
.switch {
    --false: #f54848;
    --true: #009068;
}

input[type=checkbox] {
    appearance: none;
    height: 2rem;
    width: 3.5rem;
    position: relative;
    border-radius: .2em;
    cursor: pointer;
}

input[type=checkbox]::before {
    content: '';
    display: block;
    height: 1.9em;
    width: 1.9em;
    transform: translate(-50%, -50%);
    position: absolute;
    top: 50%;
    left: calc(1.9em/2 + .3em);
    background-color: var(--false);
    border-radius: .2em;
    transition: .3s ease;
}

input[type=checkbox]:checked::before {
    background-color: var(--true);
    left: calc(100% - (1.9em/2 + .3em));
}

.switch {
    display: flex;
    flex-direction: row;
}
</style>
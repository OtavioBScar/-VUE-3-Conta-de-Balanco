<script>
export default {
    setup() {
        const transacoes = [
            { id: 1, texto: "Flores", quantidade: -23.99 },
            { id: 2, texto: "Salario", quantidade: 1442.87 },
            { id: 3, texto: "Caneca", quantidade: -14.55 },
        ];

        return {
            transacoes,
        }
    }
}
</script>

<template>
    <h3>Histórico</h3>
    <ul id="lista" class="lista">
        <li v-for="transacao in transacoes" 
        :key="transacao.id" 
        :class="transacao.quantidade < 0 ? 'minus' : 'plus'">
            {{ transacao.texto }} <span>{{ transacao.quantidade }}</span>
            <button class='delete-btn'>x</button>
        </li>
    </ul>
</template>
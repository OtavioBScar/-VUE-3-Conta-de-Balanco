<template>
    <h3>Adicionar nova transação</h3>
    <form id="form">
        <div class="form-control">
            <label for="text">Texto</label>
            <input type="text" id="text" placeholder="Adicione texto..." />
        </div>
        <div class="form-control">
            <label for="Quantidade">
                Quantidade <br/>
                {negativo = despesa, positivo - Renda}
            </label>
            <input type="number" id="quantidade" placeholder="Adicione quantidade..." />
        </div>
        <button class="btn">Adicionar transação</button>
    </form>
</template>

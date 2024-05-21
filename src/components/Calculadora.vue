<script setup>
import { reactive } from 'vue';

const estado = reactive({
    numero1: '',
    numero2: '',
    operacaoAritmetica: 'adicao',
    operacoes: {
        adicao: (a, b) => a + b,
        subtracao: (a, b) => a - b,
        multiplicacao: (a, b) => a * b,
        divisao: (a, b) => (b !== 0 ? a / b : 'Nenhum número pode ser dividido por 0'),
    },
    resultado: 0,
})

const resultadoDaOperacao = () => {
    const { numero1, numero2, operacaoAritmetica } = estado;
    estado.resultado = estado.operacoes[operacaoAritmetica](parseFloat(numero1), parseFloat(numero2));
}
</script>

<template>
    <div class="container mt-5">
        <h2>Calculadora Aritmética</h2>
        <div class="form-group">
            <label for="numero1">Número 1:</label>
            <input @input="resultadoDaOperacao" type="number" v-model="estado.numero1" class="form-control"
                id="numero1">
        </div>
        <div class="form-group mt-3">
            <label for="operacao">Operação:</label>
            <select id="operacao" v-model="estado.operacaoAritmetica" @change="resultadoDaOperacao"
                class="form-control">
                <option value="adicao">+</option>
                <option value="subtracao">-</option>
                <option value="multiplicacao">*</option>
                <option value="divisao">/</option>
            </select>
        </div>
        <div class="form-group mt-3">
            <label for="numero2">Número 2:</label>
            <input @input="resultadoDaOperacao" type="number" v-model="estado.numero2" class="form-control"
                id="numero2">
        </div>
        <div class="form-group mt-3">
            Resultado: {{ estado.resultado }}
        </div>
    </div>
</template>

<style scoped>
h2 {
    text-align: center
}

.container {
    max-width: 400px;
    margin: auto;
}
</style>

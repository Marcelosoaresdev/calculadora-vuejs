<template>
  <div>
      <h2>Calculadora Simples</h2>

      <input type="number" v-model="numero1" placeholder="Digite o primeiro número">
      <input type="number" v-model="numero2" placeholder="Digite o segundo número">

      <select v-model="operacao">
          <option value="+">Somar</option>
          <option value="-">Subtrair</option>
          <option value="*">Multiplicar</option>
          <option value="/">Dividir</option>
      </select>

      <div v-if="resultado !== null">
          <h3>Resultado: {{ resultado }}</h3>
      </div>
      <div v-else>
          <h3>Digite números válidos!</h3>
      </div>
  </div>
</template>

<script>
export default {
  data() {
      return {
          numero1: '',
          numero2: '',
          operacao: '+',
          resultado: null
      };
  },
  methods: {
      calcular() {
          const num1 = parseFloat(this.numero1);
          const num2 = parseFloat(this.numero2);

          if (isNaN(num1) || isNaN(num2)) {
              this.resultado = null;
              return;
          }

          switch (this.operacao) {
              case '+':
                  this.resultado = num1 + num2;
                  break;
              case '-':
                  this.resultado = num1 - num2;
                  break;
              case '*':
                  this.resultado = num1 * num2;
                  break;
              case '/':
                  this.resultado = num2 !== 0 ? num1 / num2 : 'Erro! Divisão por zero';
                  break;
          }
      }
  },
  watch: {
      numero1() {
          this.calcular();
      },
      numero2() {
          this.calcular();
      },
      operacao() {
          this.calcular();
      }
  }
};
</script>

<style>
body {
  font-family: Arial, sans-serif;
  max-width: 300px;
  margin: 20px auto;
}
input, select {
  width: 100%;
  padding: 5px;
  margin: 5px 0;
}
div {
  margin: 10px 0;
}
</style>

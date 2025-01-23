<script setup>
import { ref } from "vue";

const current = ref(""); // Display da calculadora

// Adiciona números ao display
const appendNumber = (number) => {
  current.value += number;
};

// Adiciona operadores ao display (substitui o último operador, se houver)
const appendOperator = (operator) => {
  // Permite adicionar o operador apenas se não houver operador no final e se não for um número (após o cálculo)
  if (current.value === "" || /[+\-*/]$/.test(current.value)) return;
  current.value += operator;
};

// Limpa o display
const clear = () => {
  current.value = "";
};

// Remove o último caractere
const deleteLast = () => {
  current.value = current.value.slice(0, -1);
};

// Calcula o resultado
const calculate = () => {
  try {
    current.value = eval(current.value) || "0"; // Calcula a expressão
  } catch {
    current.value = "Erro"; // Exibe erro no display
    setTimeout(() => (current.value = ""), 2000); // Limpa o erro após 2 segundos
  }
};
</script>

<template>
  <div class="calculator-container">
    <div class="calculator">
      <!-- Display da calculadora -->
      <div class="display">
        <span>{{ current || "0" }}</span>
      </div>
      <div class="buttons">
        <!-- Botões da calculadora -->
        <button @click="clear">C</button>
        <button @click="deleteLast">⌫</button>
        <button @click="appendOperator('/')">÷</button>
        <button @click="appendOperator('*')">×</button>

        <button @click="appendNumber('7')">7</button>
        <button @click="appendNumber('8')">8</button>
        <button @click="appendNumber('9')">9</button>
        <button @click="appendOperator('-')">-</button>

        <button @click="appendNumber('4')">4</button>
        <button @click="appendNumber('5')">5</button>
        <button @click="appendNumber('6')">6</button>
        <button @click="appendOperator('+')">+</button>

        <button @click="appendNumber('1')">1</button>
        <button @click="appendNumber('2')">2</button>
        <button @click="appendNumber('3')">3</button>
        <button @click="calculate">=</button>

        <button class="zero" @click="appendNumber('0')">0</button>
        <button @click="appendNumber('.')">.</button>
      </div>
    </div>
  </div>
</template>

<style>
/* Centraliza a calculadora */
.calculator-container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  background: linear-gradient(135deg, #1e293b, #0f172a);
}

/* Estilização da calculadora */
.calculator {
  background: #2d3748;
  padding: 20px;
  border-radius: 15px;
  box-shadow: 0 10px 20px rgba(0, 0, 0, 0.25);
  width: 320px;
}

/* Estilo do display */
.display {
  background: #1a202c;
  color: #f8fafc;
  font-size: 2rem;
  text-align: right;
  padding: 15px;
  border-radius: 10px;
  margin-bottom: 10px;
  box-sizing: border-box;
  display: flex;
  justify-content: flex-end;
  align-items: center;
}

/* Botões */
.buttons {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 10px;
}

button {
  background: #4a5568;
  color: #f8fafc;
  font-size: 1.2rem;
  border: none;
  border-radius: 10px;
  padding: 15px;
  cursor: pointer;
}

button:hover {
  background: #2c5282;
}

.zero {
  grid-column: span 2;
}
</style>

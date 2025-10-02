<template>
  <div>
    <h1>{{ mensagem }}</h1>

    <p :class ="{destaque: contadorA > contadorB}">Contador: {{ contadorA }}</p>

    <button @click="incrementarA">+1</button>
    <button @click="decrementarA">-1</button>

    <p :class ="{destaque: contadorB > contadorA}">Contador: {{ contadorB }}</p>

    <button @click="incrementarB">+1</button>
    <button @click="decrementarB">-1</button>
    
    <p>A soma dos contadores é: {{ contadoresSomados }}</p>
  </div>
</template>

<script setup>
import { ref, computed  } from 'vue'

const mensagem = ref('Atividade Contador')

const contadorA = ref(0)

const contadorB = ref(0)

function incrementarA() {
  contadorA.value++  
}

function decrementarA() {
  contadorA.value--
}

function incrementarB() {
  contadorB.value++  
}

function decrementarB() {
  contadorB.value--
}

const contadoresSomados = computed(() => contadorA.value + contadorB.value)
</script>

<style scoped>
h1 {
  color: #42b983;
  font-size: 2rem;
  text-align: center;
  margin-top: 50px;
}

p {
  text-align: center;
  font-size: 1.2rem;
  margin-top: 10px;
}

button {
  display: inline;
  margin: 10px 10px;
  padding: 5px 15px;
  font-size: 1rem;
  cursor: pointer;
}

.destaque{
  background-color: #42b983;
  color: white;
  border-radius: 10px
}
</style>

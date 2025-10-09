<template>
<form @submit.prevent="adicionarMensagem">
  <input v-model.trim="novaMensagem" placeholder="Digite a mensagem" />
  <button>Adicionar</button>
</form>

<ul v-if="estado.itens.length">
  <li v-for="m in estado.itens" :key="m.id">
    #{{ m.id }} — {{ m.texto }}
  </li>
</ul>
<p v-else>Lista vazia.</p>
</template>

<script setup>
import { reactive, ref } from 'vue'

const estado = reactive({
  nextId: 3,
  itens: [
    { id: 1, texto: 'Olá Mundo' },
    { id: 2, texto: 'Aula de Vicente' }
  ]
})

const novaMensagem = ref('')

function adicionarMensagem() {
  if (!novaMensagem.value) return
  estado.itens.push({
    id: estado.nextId++,
    texto: novaMensagem.value
  })
  novaMensagem.value = ''
}

function removerMensagem(id) {
  estado.itens = estado.itens.filter(m => m.id !== id)
}
</script>

<style scoped>
form { margin: 8px 0; }
input { padding: 6px; margin-right: 6px; }
ul { margin-top: 10px; padding-left: 20px; }
li { margin-bottom: 6px; }
button { cursor: pointer; }
</style>
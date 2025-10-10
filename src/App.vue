<template>
<form @submit.prevent="adicionarMensagem">
  <input v-model.trim="novaMensagem" placeholder="Digite a mensagem" />
  <button :disabled="!novaMensagem">Adicionar</button>
</form>
<p v-if="erro" class='erro'>{{erro}}</p>
<input type="text" v-model="filtro" placeholder="Buscar mensagem">

<p v-if='filtro'>Exibindo {{ buscar.length }} de {{estado.itens.length}}</p>

<ul v-if="estado.itens.length">
  <button class='limpar' @click="limpar">Limpar</button>
  <li :class="{ longo: m.texto.length > 30 }" v-for="m in buscar" :key="m.id">
    #{{ m.id }} — {{ m.texto }}
    <button @click = "removerMensagem(m.id)">Delete</button>
  </li>
</ul>
<p v-else>Lista vazia.</p>
</template>

<script setup>
import { reactive, computed, ref } from 'vue'

const estado = reactive({
  nextId: 3,
  itens: [
    { id: 1, texto: 'Olá Mundo' },
    { id: 2, texto: 'Aula de Vicente' }
  ]
})

const novaMensagem = ref('')
const erro = ref('')

function adicionarMensagem() {
  if (!novaMensagem.value) {
    erro.value = 'O campo não pode estar vazio.'
    return
  }
  estado.itens.push({
    id: estado.nextId++,
    texto: novaMensagem.value
  })
  novaMensagem.value = ''
  erro.value = ''
}

function removerMensagem(id) {
  estado.itens = estado.itens.filter(m => m.id !== id)
}

function limpar() {
  estado.itens = []
}

const filtro = ref('')

const buscar = computed(() => estado.itens.filter((m) => m.texto.toLowerCase().includes(filtro.value.toLowerCase())))


</script>

<style scoped>
form { margin: 8px 0; }
input { padding: 6px; margin-right: 6px; }
ul { margin-top: 10px; padding-left: 20px; }
li { margin-bottom: 6px; }
button { cursor: pointer; }
.limpar {margin-bottom: 10px}
.longo {font-weight: 800}
</style>
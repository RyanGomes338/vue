<template>
  <div class="container">
    <h1>Cadastro de Filmes</h1>

    <!-- Dados do usuário -->
    <h2>Dados do Usuário</h2>
    <input v-model="nome" placeholder="Nome" />
    <input v-model="curso" placeholder="Curso" />
    <input v-model="cidade" placeholder="Cidade" />

    <p><strong>Nome:</strong> {{ nome }}</p>
    <p><strong>Curso:</strong> {{ curso }}</p>
    <p><strong>Cidade:</strong> {{ cidade }}</p>

    <hr />

    <!-- Cadastro de filmes -->
    <h2>Cadastrar Filme</h2>
    <input
      v-model="novoFilme"
      placeholder="Digite o nome do filme"
      @keyup.enter="adicionarFilme"
    />
    <button @click="adicionarFilme">Adicionar</button>

    <!-- Lista de filmes -->
    <h2>Lista de Filmes</h2>

    <ul>
      <li v-for="(filme, index) in filmes" :key="index">
        <span :class="{ assistido: filme.assistido }">
          {{ filme.nome }}
        </span>

        <button @click="toggleAssistido(index)">
          {{ filme.assistido ? 'Assistido' : 'Não assistido' }}
        </button>

        <button @click="removerFilme(index)">Remover</button>
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref } from 'vue'

// Dados do usuário
const nome = ref('')
const curso = ref('')
const cidade = ref('')

// Campo do novo filme
const novoFilme = ref('')

// Lista de filmes
const filmes = ref([])

// Adicionar filme
function adicionarFilme() {
  if (novoFilme.value.trim() !== '') {
    filmes.value.push({
      nome: novoFilme.value,
      assistido: false
    })

    novoFilme.value = ''
  }
}

// Marcar/desmarcar como assistido
function toggleAssistido(index) {
  filmes.value[index].assistido =
    !filmes.value[index].assistido
}

// Remover filme
function removerFilme(index) {
  filmes.value.splice(index, 1)
}
</script>

<style>
.container {
  max-width: 600px;
  margin: auto;
  font-family: Arial, sans-serif;
}

input {
  margin: 5px;
  padding: 8px;
}

button {
  margin-left: 5px;
  padding: 6px 10px;
}

.assistido {
  text-decoration: line-through;
  color: green;
  font-weight: bold;
}
</style>
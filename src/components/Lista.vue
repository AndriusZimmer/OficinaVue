<script setup>
import { ref } from 'vue'

const msg = ref('Lista de Jogos')
const msgVazia = ref('A lista de jogos está vazia, adicione um jogo.')

let id = 1

let novoJogo = ref('')

let jogos = ref([
  { id: id++, text: 'Pokemon' },
  { id: id++, text: 'Valorant' },
  { id: id++, text: 'Minecraft' },
])

function adicionarJogo() {
  jogos.value.push({ id: id++, text: novoJogo.value })
  novoJogo.value = ''
}

function removerJogo(jogo) {
  jogos.value = jogos.value.filter((t) => t !== jogo)
}
</script>

<template>
  <div class="container text-center">
    <h1 class="main-title-xl">{{ msg }}</h1>
    <form @submit.prevent="adicionarJogo">
      <div class="row py-2 justify-content-center align-items-center">
        <div class="col-12 col-md-6 col-lg-4">
          <input
            class="form-control form-control-sm"
            v-model="novoJogo"
            required
            placeholder="Adicione um jogo"
          />
        </div>
        <div class="col-12 col-md-auto mt-2 mt-md-0">
          <button class="btn btn-primary" type="submit">Adicionar Jogo</button>
        </div>
      </div>
    </form>
    <h2 class="main-title-l" v-show="jogos.length === 0">{{ msgVazia }}</h2>
    <ul class="list-group">
      <li
        class="list-group-item d-flex justify-content-between align-items-center"
        :class="{ 'bg-secondary': jogo.id % 2 === 0 }"
        v-for="jogo in jogos"
      >
        {{ jogo.text }}
        <button class="btn btn-danger btn-sm" @click="removerJogo(jogo)">X</button>
      </li>
    </ul>
  </div>
</template>

<style scoped></style>

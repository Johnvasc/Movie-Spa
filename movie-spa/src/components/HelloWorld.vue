<script setup>
import { ref } from 'vue'

const nome = ref('')
const curso = ref('')
const cidade = ref('')
const cadastrado = ref(false)
const novoFilme = ref('')
const filmes = ref([])

function submitForm() {
  cadastrado.value = true
}

function addFilme() {
  if (novoFilme.value.trim() !== '') {
    filmes.value.push({
      nome: novoFilme.value,
      assistido: false
    })
    novoFilme.value = ''
  }
}
</script>

<template>
  <nav v-if="cadastrado">
    <h1>Olá, {{ nome }}!</h1>
    <p>{{ curso }} 🎓</p>
    <p>{{ cidade }} 🌏</p>
  </nav>

  <div id="naoCadastrado" v-else>
    <form @submit.prevent="submitForm">
      <label for="nome">Nome:</label>
      <input type="text" id="nome" v-model="nome" required />

      <label for="curso">Curso:</label>
      <input type="text" id="curso" v-model="curso" required />

      <label for="cidade">Cidade:</label>
      <input type="text" id="cidade" v-model="cidade" required />
      <button type="submit">Enviar</button>
    </form>
  </div>

  <div id="listaFilmesContainer" v-if="cadastrado">
    <h2>Lista de Filmes</h2>
    <input type="text" v-model="novoFilme" placeholder="Adicionar novo filme" />
    <button @click="addFilme"> Adicionar Filme </button>
    <ul id="listaFilmes">
      <li class="filme" v-for="(filme, index) in filmes" :key="index">
        {{ filme.nome }}
        <div>
          <input type="checkbox" v-model="filme.assistido" @click="filme.assistido = !filme.assistido" />
          <label for="assistido">Assistido</label>
        </div>
        <button @click="filmes.splice(index, 1)">Remover</button>
      </li>
    </ul>
  </div>

</template>

<style scoped>
form {
  display: flex;
  flex-direction: column;
  max-width: 300px;
  margin: 0 auto;
}
label {
  margin-top: 10px;
}
input {
  padding: 5px;
  margin-top: 5px;
}
button {
  margin-top: 15px;
  padding: 10px;
  background-color: #42b983; 
  color: white;
  border: none;
  cursor: pointer;
}
button:hover {
  background-color: #369870;
}
nav {
  text-align: center;
  margin-top: 1rem;
  display: flex;
  flex-direction: column;
  align-items: center;

}
#naoCadastrado form{
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: 3rem;
  border: 1px solid #ccc;
  border-radius: 5px;
  padding: 3.5rem 2rem;

}
#listaFilmesContainer {
  width: 90%;
  max-width: 700px;
  margin: 40px auto;
  padding: 25px;
  border-radius: 15px;
  box-shadow: 0 8px 20px rgba(0,0,0,.12);
}

#listaFilmesContainer h2 {
  text-align: center;
  margin-bottom: 20px;
  color: #42b983;
}

#listaFilmesContainer input[type="text"] {
  width: calc(100% - 130px);
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 8px;
  font-size: 15px;
}

#listaFilmesContainer > button {
  width: 110px;
  margin-left: 10px;
  padding: 10px;
  border: none;
  border-radius: 8px;
  background: #42b983;
  color: white;
  cursor: pointer;
  transition: .2s;
}

#listaFilmesContainer > button:hover {
  background: #369870;
}

#listaFilmes {
  list-style: none;
  padding: 0;
  margin-top: 25px;
}

.filme {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 15px;
  margin-bottom: 12px;
  border-radius: 10px;
  transition: .2s;
}

.filme:hover {
  transform: translateY(-2px);
  box-shadow: 0 3px 10px rgba(0,0,0,.08);
}

.filme div {
  display: flex;
  align-items: center;
  gap: 8px;
}

.filme button {
  background: #e74c3c;
  color: white;
  border: none;
  padding: 8px 14px;
  border-radius: 8px;
  cursor: pointer;
  transition: .2s;
}

.filme button:hover {
  background: #c0392b;
}

.filme input[type="checkbox"] {
  width: 18px;
  height: 18px;
  cursor: pointer;
}
</style>

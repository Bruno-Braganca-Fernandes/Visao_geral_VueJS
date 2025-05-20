<script setup>
import { reactive } from "vue";

const nome = "Bruno Bragança";
const meuObj = {
  nome: "Bruno",
  filmeFavorito: "Batman",
};

function dizOla(nome) {
  return `${nome} diz oi`;
}

const enderecoImagemBatman ="https://areajugones.sport.es/wp-content/uploads/2019/03/The-Batman-DC-Comics.jpg"
  
const imagemSuperman = "https://tse2.mm.bing.net/th?id=OIP.ABjH3exmspN8jeJYGkzyCAHaFn&pid=Api&P=0&h=180"

const botaoEstaDesabilitado = false;

const gostaDoBatman = false
const gostaDoSuperman = false

const estaAutorizado = true

// let contador = 0
const estado = reactive({
  contador: 0,
  email: '',
})

function incrementar() {
  estado.contador++
}

function decrementar() {
  estado.contador--
}

function alteraEmail(evento) {
  estado.email = evento.target.value
}
</script>

<template>
  <h1>{{ dizOla("Bruno") }}</h1>
  <img v-if="gostaDoBatman" :src="enderecoImagemBatman" alt="" />
  <img v-else-if="gostaDoSuperman" :src="imagemSuperman" alt="">
  <h2 v-else>Não curte heróis da DC</h2>

  <h1 v-if="estaAutorizado">Bem vindo</h1>
  <h1 v-else>Não possui acesso</h1>

  <button :disabled="botaoEstaDesabilitado">enviar mensagem</button>

  <br>
  <hr>

  {{ estado.contador }}

<button @click="incrementar" type="button">+</button>
<button @click="decrementar" type="button">-</button>

  <br>
  <hr>

{{ estado.email }}
<input type="email" @keyup="alteraEmail">

</template>

<style scoped></style>

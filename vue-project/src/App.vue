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
  saldo: 5000,
  transferindo: 0,
  nomes: ['Bruno', 'Dafny', 'Abelardo', 'Betania'],
nomeAInserir: ''

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

function mostraSaldoFuturo() {
  const {saldo, transferindo} = estado
  return saldo - transferindo
}

function validaValorTranferencia() {
    const {saldo, transferindo} = estado
  return saldo >= transferindo
}

function cadastraNome() {
  if(estado.nomeAInserir.length >= 3){
    estado.nomes.push(estado.nomeAInserir)
  } else {
    alert("Digite mais caracteres")
  }
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

  <br>
  <hr>

  Saldo: {{ estado.saldo }} <br>
  Transferindo: {{ estado.transferindo }} <br>
  Saldo depois da transferência: {{ mostraSaldoFuturo() }} <br>
  <input class="campo" :class="{ invalido: !validaValorTranferencia() }" @keyup="evento => estado.transferindo = evento.target.value" type="number" placeholder="Quantia para transferir">
<button v-if="validaValorTranferencia()">Transferir</button>
<span v-else>Valor maior que o saldo</span>

<br> <hr>

<ul>
  <li v-for="nome in estado.nomes">
    {{ nome }}
  </li>
</ul>
<input @keyup="evento => estado.nomeAInserir = evento.target.value" type="text" placeholder="Digite um novo nome">
<button @click="cadastraNome()" type="button">Cadastrar nome</button>

<h3 v-for="nome in estado.nomes">{{ nome }}</h3>
</template>

<style scoped>
img{
  max-width: 200px;
}

.invalido{
  outline-color:red ;
  border-color: red;
}

.campo{
  border: 2px solid #000;
}

</style>

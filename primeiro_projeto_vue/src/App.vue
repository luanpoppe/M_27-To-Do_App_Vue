<script setup>
import { reactive } from 'vue';

  const nome = "gian souza"
  const meuObj = {
    nome: "gian",
    filmeFavorito: "Rocky"
  }

  function dizOlá(nome) {
    return `${nome} diz oi`
  }

  const endereçoDaImagemDoBatman = "https://images.unsplash.com/photo-1531259683007-016a7b628fc3?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8MXx8YmF0bWFufGVufDB8fDB8fHww&w=1000&q=80"
  const ImagemDoSuperman = "https://observatoriodocinema.uol.com.br/wp-content/uploads/2022/10/superman-dc-comics-1200x900-1.jpg"

  const gostaDoBatman = false
  const gostaDoSuperman = false

  const estaAutorizado = false

  // let contador = 0
  const estado = reactive({
    contador: 0,
    email: "",
    saldo: 5000,
    transferindo: 0,
    nomes: ["gian", "paulo", "luisa", "monica"],
    nomeAInserir: ","
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
    const { saldo, transferindo} = estado
    return saldo - transferindo
  }

  function validaValorTransferencia() {
    const { saldo, transferindo} = estado
    return saldo >= transferindo
  }

function cadastrarNome() {
  if (estado.nomeAInserir.length >= 3) {
    estado.nomes.push(estado.nomeAInserir)
  } else {
    alert("Digite mais caracteres")
  }
}

</script>

<template>
  <h1>{{ dizOlá("paula") }}</h1>
  <img v-if="gostaDoBatman" :src="endereçoDaImagemDoBatman" alt="">
  <img v-else-if="gostaDoSuperman" :src="ImagemDoSuperman" alt="">
  <h2 v-else>Não curte heróis da DC</h2>

  <h1 v-if="estaAutorizado">Bem-vindo</h1>
  <h1 v-else>Não possui acesso</h1>

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
  <input class="campo" :class="{ invalido: !validaValorTransferencia()}" @keyup="evento => estado.transferindo = evento.target.value" type="number" placeholder="Quantia para transferir">
  <button v-if="validaValorTransferencia()">Transferir</button>
  <span v-else>Valor maior que o saldo</span>

  <br>
  <hr>

  <ul>
    <li v-for="nome in estado.nomes">
      {{ nome }}
    </li>
  </ul>
  <input @keyup="evento => estado.nomeAInserir = evento.target.value" type="text" placeholder="Digite um novo nome">
  <button @click="cadastrarNome" type="button">Cadastrar nome</button>

  <h3 v-for="nome in estado.nomes">{{ nome }}</h3>

</template>

<style scoped>
  img{
    max-width: 200px;
  }

  .invalido {
    outline-color: red;
    border-color: red;
  }

  .campo{
    border: 2px solid black;
  }
</style>

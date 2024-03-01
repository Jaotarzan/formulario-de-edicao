<script setup>
import { ref, reactive } from 'vue'
import name from './components/cadastro_usuario/name.vue'
import email from './components/cadastro_usuario/email.vue'
import languages from './components/cadastro_usuario/languages.vue'
import adress from './components/cadastro_usuario/adress.vue';
import age from './components/cadastro_usuario/age.vue'
import bio from './components/cadastro_usuario/bio.vue'
import city from './components/cadastro_usuario/city.vue'
import hobbies from './components/cadastro_usuario/hobbies.vue'
import password from './components/cadastro_usuario/password.vue'

const i = ref(0)
const show = ref(false)
const pessoa = reactive({
  nome: String,
  idade: Number,
  email: String,
  senha: String,
  cidade: String,
  endereco: String,
  hobbies: String,
  linguagens: String,
  biografia: String
})

function enviarDados() {
  i.value++
  console.log(pessoa.nome)
  mostrarMsg()
}

function mostrarMsg() {
  show.value = true
  setTimeout(() => {
    show.value = false
  }, 1000)
}

const nomear = (nome) => {
  pessoa.nome = nome
  debugger
}
</script>

<template>
  <div class="form">
    <h1>Formulário</h1>
    <form @submit.prevent="enviarDados">
      <name @EnviarNome="nomear" />
      <email />
      <password />
      <age />
      <city />
      <adress />
      <hobbies />
      <languages />
      <bio />
      <div>
        <input type="submit" value="enviar dados" />
      </div>
    </form>
  </div>
  <div class="msg" v-if="show">
    <h1>usuário cadastrado</h1>
  </div>
</template>

<style scoped>
.msg {
  background-color: rgba(93, 157, 199, 0.767);
  border-radius: 20px;
  border: 2px solid rgb(58, 135, 170);
  width: 100%;
}

p,
h1 {
  margin: 2%;
}
</style>

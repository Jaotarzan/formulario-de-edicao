<script setup>
import { ref, reactive } from 'vue'

const estados = [
  { sigla: 'AC', name: 'Acre' },
  { sigla: 'AL', name: 'Alagoas' },
  { sigla: 'AP', name: 'Amapá' },
  { sigla: 'AM', name: 'Amazonas' },
  { sigla: 'BA', name: 'Bahia' },
  { sigla: 'CE', name: 'Ceará' },
  { sigla: 'DF', name: 'Distrito Federal' },
  { sigla: 'ES', name: 'Espírito Santo' },
  { sigla: 'GO', name: 'Goiás' },
  { sigla: 'MA', name: 'Maranhão' },
  { sigla: 'MT', name: 'Mato Grosso' },
  { sigla: 'MS', name: 'Mato Grosso do Sul' },
  { sigla: 'MG', name: 'Minas Gerais' },
  { sigla: 'PA', name: 'Pará' },
  { sigla: 'PB', name: 'Paraíba' },
  { sigla: 'PR', name: 'Paraná' },
  { sigla: 'PE', name: 'Pernambuco' },
  { sigla: 'PI', name: 'Piauí' },
  { sigla: 'RJ', name: 'Rio de Janeiro' },
  { sigla: 'RN', name: 'Rio Grande do Norte' },
  { sigla: 'RS', name: 'Rio Grande do Sul' },
  { sigla: 'RO', name: 'Rondônia' },
  { sigla: 'RR', name: 'Roraima' },
  { sigla: 'SC', name: 'Santa Catarina' },
  { sigla: 'SP', name: 'São Paulo' },
  { sigla: 'SE', name: 'Sergipe' },
  { sigla: 'TO', name: 'Tocantins' }
]

const hobbies = reactive([
  { id: 1, hobbie: 'Esporte' },
  { id: 2, hobbie: 'Leitura' },
  { id: 3, hobbie: 'Surf' },
  { id: 4, hobbie: 'Viajar' }
])

const linguagens = reactive([
  { id: 1, tipo: 'Java' },
  { id: 2, tipo: 'C++' },
  { id: 3, tipo: 'Python' },
  { id: 4, tipo: 'Php' }
])

const pessoa = reactive({
  Nome: '',
  Idade: 18,
  Email: '',
  Senha: '',
  Estado: '',
  Cidade: '',
  Endereco: '',
  Hobbies: [],
  Linguagens: [],
  Biografia: ''
})

const show = ref(false)
const senhaVerificada = ref('')

function EnviarDados() {
  if (senhaVerificada.value == pessoa.senha) {
    show.value = true
  } else {
    alert('As senhas não correspodem corretamente!')
    document.getElementById('senhaConfirma').focus()
  }
}
</script>

<template>
  <div>
    <h1>Formulário de Edição</h1>
    <div id="usuario" v-if="show">
      <p v-for="(dado, key) of pessoa" :key="key">{{ key }}: {{ dado }}</p>
      <button @click="show = false" class="submit">voltar</button>
    </div>
    <form v-else @submit.prevent="EnviarDados">
      <div class="input-container">
        <div class="input-title">
          <label for="nome">Digite seu nome:</label>
        </div>
        <div>
          <input
            type="text"
            v-model="pessoa.nome"
            minlength="3"
            maxlength="20"
            autocomplete="on"
            required
          />
        </div>
      </div>

      <div class="input-container">
        <div class="input-title">
          <label for="email">Digite seu email:</label>
        </div>
        <input type="email" v-model="pessoa.email" maxlength="50" autocomplete="on" required />
      </div>
      <div class="input-container">
        <div class="input-title">
          <label for="senha">Digita a sua senha:</label>
        </div>
        <input type="password" v-model="pessoa.senha" minlength="8" required />
      </div>
      <div class="input-container">
        <div class="input-title">
          <label for="senhaConfirma">Confirme a sua senha:</label>
        </div>
        <input
          type="password"
          id="senhaConfirma"
          v-model="senhaVerificada"
          minlength="8"
          required
        />
      </div>
      <div class="input-container">
        <div class="input-title">
          <label for="idade">Digite a sua idade:</label>
        </div>
        <input type="number" v-model="pessoa.idade" min="18" max="60" required />
      </div>
      <div class="input-container">
        <div class="input-title">
          <label for="hobbies">Informe o seu estado:</label>
        </div>
        <select v-model="pessoa.estado">
          <option v-for="estado in estados" :key="estado.sigla" :value="estado.sigla">
            {{ estado.name }}
          </option>
        </select>
      </div>
      <div class="input-container">
        <div class="input-title">
          <label for="cidade">Informe a sua cidade:</label>
        </div>
        <input type="text" v-model="pessoa.cidade" />
      </div>
      <div class="input-container">
        <div class="input-title">
          <label for="cidade">Informe o seu endereço:</label>
        </div>
        <input type="text" v-model="pessoa.endereco" />
      </div>
      <div class="check-container">
        <div class="input-title">
          <label for="hobbies">Informe quais são os seus hobbies:</label>
        </div>
        <div class="opcao-checkbox" v-for="passatempo in hobbies" :key="passatempo.id">
          <input
            type="checkbox"
            name="hobbies"
            :value="passatempo.hobbie"
            v-model="pessoa.hobbies"
          />
          <span>{{ passatempo.hobbie }}</span>
        </div>
      </div>
      <div class="check-container">
        <div class="input-title">
          <label for="linguagens">Informe quais são as linguagens que você domina:</label>
        </div>
        <div class="opcao-checkbox" v-for="linguagem in linguagens" :key="linguagem.id">
          <input
            type="checkbox"
            name="hobbies"
            :value="linguagem.tipo"
            v-model="pessoa.linguagens"
          />
          <span>{{ linguagem.tipo }}</span>
        </div>
      </div>
      <div class="bio-container">
        <div class="input-title">
          <label for="email">Faça uma breve autobiografia:</label>
        </div>
        <textarea v-model="pessoa.biografia"></textarea>
      </div>

      <div class="submit-container">
        <input type="submit" value="Enviar dados" class="submit" />
      </div>
    </form>
  </div>
</template>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Roboto:ital,wght@0,100;0,300;0,400;0,500;0,700;0,900;1,100;1,300;1,400;1,500;1,700;1,900&display=swap');

* {
  margin: 0%;
  padding: 0%;
  font-family: 'Roboto', sans-serif;
}

p,
h1 {
  margin: 2%;
}

h1 {
  text-align: center;
}

form {
  flex-wrap: wrap;
  display: flex;
  margin-left: 4%;
}

input,
select {
  border-radius: 7px;
  border: 1px solid rgb(46, 44, 44);
  width: 80%;
  height: 4vh;
  font-size: 13px;
}

.input-title {
  margin: 7px;
  border-left: 3px solid #3ebc32;
  width: 100%;
}

.input-container {
  width: 25%;
  height: 20vh;
}

.check-container {
  display: flex;
  flex-wrap: wrap;
  width: 50%;
}

.opcao-checkbox {
  display: flex;
  align-items: flex-start;
  flex-direction: row;
  width: 40%;
  margin-bottom: 10px;
}

.opcao-checkbox span,
.opcao-checkbox input {
  width: auto;
}

.opcao-checkbox span {
  margin-top: 4px;
  margin-left: 6px;
  font-weight: bold;
}

label {
  font-size: 16px;
  margin-left: 5px;
}

#usuario {
  text-align: center;
}

.bio-container {
  width: 60%;
  height: 20vh;
}

.submit-container {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 40%;
}

.submit {
  width: 30%;
  height: 7vh;
  margin-top: 10vh;
  background-color: #3ebc32;
  color: white;
  border: none;
  cursor: pointer;
  font-size: 17px;
}

.submit:hover {
  background-color: #3ea534;
}

textarea {
  width: 100%;
  height: 100%;
}
</style>

<script setup>
import { ref } from 'vue'

const nome = ref('')

defineEmits(['EnviarNome'])
</script>

<template>
  <label for="nome">Digite seu nome:</label>
  <div>
    <input
      type="text"
      v-model="nome"
      @submit="$emit('EnviarNome', nome)"
      minlength="3"
      maxlength="20"
      autocomplete="on"
      required
    />
  </div>
</template>

<style scoped></style>

<script setup>
import { ref } from 'vue'

const formData = ref({
  nombre: '',
  apellido: '',
  correo: '',
  edad: ''
})

const getEtapa = (edad) => {
  const edadNum = parseInt(edad)
  if (!edadNum) return ''
  if (edadNum >= 0 && edadNum <= 13) return 'Niñez'
  if (edadNum >= 14 && edadNum <= 17) return 'Adolescencia'
  if (edadNum >= 18 && edadNum <= 35) return 'Adultos jóvenes'
  if (edadNum >= 35 && edadNum <= 64) return 'Adulto'
  if (edadNum >= 65) return 'Tercera edad'
  return ''
}
</script>

<template>
  <div class="container">
    <h1>Formulario Personal</h1>
    
    <form @submit.prevent class="form">
      <div class="form-group">
        <label>Nombre:</label>
        <input type="text" v-model="formData.nombre" placeholder="Ingrese su nombre">
      </div>

      <div class="form-group">
        <label>Apellido:</label>
        <input type="text" v-model="formData.apellido" placeholder="Ingrese su apellido">
      </div>

      <div class="form-group">
        <label>Correo:</label>
        <input type="email" v-model="formData.correo" placeholder="Ingrese su correo">
      </div>

      <div class="form-group">
        <label>Edad:</label>
        <input type="number" v-model="formData.edad" placeholder="Ingrese su edad">
      </div>
    </form>

    <div v-if="formData.nombre && formData.apellido && formData.correo" class="result">
      <h2>Saludo:</h2>
      <p>¡Hola {{ formData.nombre }} {{ formData.apellido }}! Tu correo es {{ formData.correo }}.</p>
    </div>

    <div v-if="formData.edad" class="result">
      <h2>Clasificación por edad:</h2>
      <p>Con {{ formData.edad }} años, te encuentras en la etapa de: <strong>{{ getEtapa(formData.edad) }}</strong></p>
    </div>
  </div>
</template>

<style scoped>
.container {
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
}

.form {
  display: flex;
  flex-direction: column;
  gap: 15px;
  margin-bottom: 20px;
}

.form-group {
  display: flex;
  flex-direction: column;
  gap: 5px;
}

label {
  font-weight: bold;
}

input {
  padding: 8px;
  border: 1px solid #ccc;
  border-radius: 4px;
  font-size: 16px;
}

.result {
  margin-top: 20px;
  padding: 15px;
  background-color: #f0f0f0;
  border-radius: 4px;
}

h1 {
  margin-bottom: 20px;
}

h2 {
  font-size: 1.2em;
  margin-bottom: 10px;
}
</style>

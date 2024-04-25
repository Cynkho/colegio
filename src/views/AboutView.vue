<script setup>
import { ref } from 'vue'
import colegio from '../content/colegio.json'

const cole = ref(colegio)

const dni = ref('')
const nombre = ref('')
const isEditing = ref(false)

function anadirAlumno(){
  isEditing.value = false
  cole.value.alumnos[dni.value] = {nombre: nombre.value}
  nombre.value = ''
  dni.value = ''
}

function borrarAlumno(dni){
  delete cole.value.alumnos[dni]
}

function editarAlumno(dniEditable){
  isEditing.value = true
  dni.value = dniEditable
  nombre.value = cole.value.alumnos[dniEditable].nombre
}

</script>

<template>
  <div class="about">
    <h1>This is an about page</h1>
    <!-- {{ colegio }} -->
  </div>
  <br>
  <hr>
  <br>
  <form @submit.prevent="anadirAlumno">
    <input v-model="dni" type="text" placeholder="DNI" :disabled="isEditing">
    <input v-model="nombre" type="text" placeholder="Nombre">
    <button class="anadir" type="submit">
      <img src="@/assets/axolotl.png" alt="ajolote">
    </button>
  </form>
  <br>
  <hr>
  <br>
  <ul>
    <li v-for="(alumno, dni) in cole.alumnos" :key="dni">
      {{ dni }}: {{ alumno.nombre }}
      <div class="botones-lista">
        <button class="editar-button" @click="editarAlumno(dni)">
          🔄️
        </button>
        <button class="del-button" @click="borrarAlumno(dni)">
          x
        </button>
      </div>
    </li>
  </ul>
</template>

<style scope>
@media (min-width: 1024px) {
  .about {
    min-height: 100vh;
    display: flex;
    align-items: center;
  }
}

form{
  display: flex;
  align-items: center;
}

.anadir{
  background: none;
  margin-left: 8px;
  padding: 3px 8px;
}

.anadir img{
  height: 64px;
  cursor: pointer;
}

.botones-lista{
  display: flex;
  justify-content: space-between;
  column-gap: 4px; 
}

li{
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  max-width: 350px;
}

</style>

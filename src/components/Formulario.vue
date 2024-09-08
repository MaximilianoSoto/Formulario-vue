<script setup>
import { reactive, ref } from 'vue'
import Alerta from "./Alerta.vue"
import { uid } from 'uid'

const alerta = reactive({
  tipo: '',
  mensaje: ''
})

const emit = defineEmits(['añadir-paciente'])

const formulario = reactive({
  nombre: '',
  propietario: '',
  email: '',
  alta: '',
  sintomas: ''
})

const validar = () => {
  const camposVacios = Object.values(formulario).some(campo => campo === '');
  
  if (camposVacios) {
    alerta.mensaje = 'Todos los campos son obligatorios';
    alerta.tipo = 'error';
    return;
  }

  
  emit('añadir-paciente', { ...formulario, id: uid() })
  alerta.mensaje = 'Usuario agregado'
  alerta.tipo = 'exito'

  // Limpiar el formulario
  Object.keys(formulario).forEach(key => formulario[key] = '')

  setTimeout(()=> {
    alerta.mensaje = ''
    alerta.tipo = ''
  },3000)
 
}
</script>

<template>
  <div class="md:w-1/2">
    <h2 class="font-black text-3xl text-center">Seguimiento Pacientes</h2>
    <p class="text-lg mt-5 text-center mb-10">
      Añade Pacientes y <span class="text-indigo-600 font-bold">Administralos</span>
    </p>

    <Alerta
      v-if="alerta.mensaje"
      :alerta="alerta"
    />

    <form class="bg-white shadow-md rounded-lg py-10 px-5" @submit.prevent="validar">
      <div class="mb-5">
        <label
          for="mascota"
          class="block text-gray-700 uppercase font-bold"
        >
          Nombre de mascota 
        </label>
        <input
          id="mascota"
          v-model="formulario.nombre"
          type="text"
          placeholder="Nombre de la mascota"
          class="border-2 w-full p-2 mt-3 placeholder-indigo-400 rounded-md"
        >
      </div>
      <div class="mb-5">
        <label
          for="propietario"
          class="block text-gray-700 uppercase font-bold"
        >
          Nombre del propietario
        </label>
        <input
          id="propietario"
          v-model="formulario.propietario"
          type="text"
          placeholder="Nombre del propietario"
          class="border-2 w-full p-2 mt-3 placeholder-indigo-400 rounded-md"
        >
      </div>
      <div class="mb-5">
        <label
          for="email"
          class="block text-gray-700 uppercase font-bold"
        >
          Email
        </label>
        <input
          id="email"
          v-model="formulario.email"
          type="email"
          placeholder="Email del propietario"
          class="border-2 w-full p-2 mt-3 placeholder-indigo-400 rounded-md"
        >
      </div>
      <div class="mb-5">
        <label
          for="alta"
          class="block text-gray-700 uppercase font-bold"
        >
          Alta
        </label>
        <input
          id="alta"
          v-model="formulario.alta"
          type="date"
          class="border-2 w-full p-2 mt-3 placeholder-indigo-400 rounded-md"
        >
      </div>
      <div class="mb-5">
        <label
          for="sintomas"
          class="block text-gray-700 uppercase font-bold"
        >
          Síntomas
        </label>
        <textarea
          id="sintomas"
          v-model="formulario.sintomas"
          placeholder="Describe los síntomas"
          class="border-2 w-full p-2 mt-3 placeholder-indigo-400 rounded-md"
        />
      </div>

      <input 
        type="submit"
        class="bg-indigo-600 w-full p-3 text-white uppercase font-bold hover:bg-indigo-400 cursor-pointer transition-colors"
        value="Registrar paciente"
      >
    </form>
  </div>
</template>
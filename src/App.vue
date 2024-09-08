<script setup>
import { ref } from 'vue'
import Header from './components/Header.vue'
import Formulario from './components/Formulario.vue'
import Paciente from './components/Paciente.vue'

const pacientes = ref([])

const añadirPaciente = (nuevoPaciente) => {
  pacientes.value.push(nuevoPaciente)
}

const eliminarPaciente = (id) => {
  pacientes.value = pacientes.value.filter(paciente => paciente.id !== id)
}

const editarPaciente = (pacienteActualizado) => {

 
  const pacienteFiltrado = pacientes.value.filter(paciente => paciente.id === pacienteActualizado.id)[0]

 

  
  /*
  pacientes.value = pacientes.value.map(paciente => 
    paciente.id === pacienteActualizado.id ? pacienteActualizado : paciente
  )*/
}
</script>

<template>
  <div class="container mx-auto mt-20">
    <Header />

    <div class="mt-12 md:flex">
      <Formulario @añadir-paciente="añadirPaciente" />

      <div class="md:w-1/2 md:h-screen overflow-y-scroll">
        <h3 class="font-black text-3xl text-center">Administra tus pacientes</h3>

        <div v-if="pacientes.length > 0">
          <p class="text-lg mt-5 text-center mb-10">
            Información de <span class="text-indigo-600 font-bold">Pacientes</span>
          </p>
          
          <Paciente
            v-for="paciente in pacientes"
            :key="paciente.id"
            :paciente="paciente"
            @eliminar-paciente="eliminarPaciente"
            @editar-paciente="editarPaciente"
          />
        </div>

        <p v-else class="mt-20 text-2xl text-center">No Hay Pacientes</p>
      </div>
    </div>
  </div>
</template>
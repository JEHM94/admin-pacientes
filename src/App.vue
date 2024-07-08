<script setup>
import { ref, reactive, onMounted, watch } from 'vue'
import { uid } from 'uid'
import Header from './components/Header.vue'
import Formulario from './components/Formulario.vue'
import Paciente from './components/Paciente.vue'


const pacientes = ref([])

const paciente = reactive({
  id: null,
  nombre: '',
  propietario: '',
  email: '',
  alta: '',
  sintomas: ''

})

watch(pacientes, () => {
  guardarLocalStorage()
}, {
  deep: true
})

onMounted(() => {
  pacientes.value = localStorage.getItem('pacientes') ? JSON.parse(localStorage.getItem('pacientes')) : []
})

const guardarLocalStorage = () => {
  localStorage.setItem('pacientes', JSON.stringify(pacientes.value))
}

const guardarPaciente = () => {
  // Edicion de paciente
  if (paciente.id) {
    const { id } = paciente
    const index = pacientes.value.findIndex(paciente => paciente.id === id)
    pacientes.value[index] = { ...paciente }
  } else {
    // Nuevo Paciente
    pacientes.value.unshift({
      ...paciente,
      id: uid()
    })
  }

  Object.assign(paciente, {
    id: null,
    nombre: '',
    propietario: '',
    email: '',
    alta: '',
    sintomas: ''
  })
}

const actualizarPaciente = (id) => {
  const pacienteEditar = pacientes.value.filter((paciente) => id === paciente.id)[0]
  Object.assign(paciente, pacienteEditar)
}

const eliminarPaciente = (id) => {
  pacientes.value = pacientes.value.filter((paciente) => paciente.id !== id)
}

</script>

<template>
  <div class="container mx-auto mt-20">
    <Header />

    <div class="mt-12 md:flex mx-5 md:mx-0">
      <Formulario v-model:nombre="paciente.nombre" v-model:propietario="paciente.propietario"
        v-model:email="paciente.email" v-model:alta="paciente.alta" v-model:sintomas="paciente.sintomas"
        @guardar-paciente="guardarPaciente" :id="paciente.id" />

      <div class="md:w-1/2">
        <h3 class="font-black  text-3xl text-center">Administra tus pacientes</h3>

        <div v-if="pacientes.length > 0">

          <p class="text-lg mt-5 text-center mb-10 ">
            Pacientes
            <span class="text-emerald-400 font-bold">Registrados</span>
          </p>

          <div class="md:h-screen overflow-y-scroll">
            <Paciente v-for="paciente in pacientes" :paciente="paciente" @actualizar-paciente="actualizarPaciente"
              @eliminar-paciente="eliminarPaciente" />
          </div>
        </div>
        <p v-else class="my-20 text-2xl text-center">No hay pacientes</p>
      </div>
    </div>
  </div>

</template>

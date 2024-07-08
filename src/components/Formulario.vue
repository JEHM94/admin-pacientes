<script setup>
import { reactive, computed } from 'vue'
import Alerta from './Alertas.vue'

const alerta = reactive({
    tipo: '',
    mensaje: ''
})

const emit = defineEmits(['update:nombre', 'update:propietario', 'update:email', 'update:alta', 'update:sintomas', 'guardar-paciente'])

const props = defineProps({
    id: {
        type: [String, null],
        required: true
    },
    nombre: {
        type: String,
        required: true
    },
    propietario: {
        type: String,
        required: true
    },
    email: {
        type: String,
        required: true
    },
    alta: {
        type: String,
        required: true
    },
    sintomas: {
        type: String,
        required: true
    }
})

const validar = () => {
    if (Object.values(props).includes('')) {
        alerta.tipo = 'error'
        alerta.mensaje = 'Todos los campos son obligatorios'
        return
    }

    emit('guardar-paciente')

    alerta.mensaje = 'Paciente registrado exitosamente'
    alerta.tipo = 'exito'

    setTimeout(() => {
        alerta.mensaje = ''
        alerta.tipo = ''
    }, 3000);
}

const editando = computed(() => props.id)
</script>

<template>
    <div class="md:w-1/2">
        <h2 class="font-black text-3xl text-center ">Registro</h2>

        <p class="text-lg mt-5 text-center mb-10 ">
            Añade Pacientes y
            <span class="text-emerald-400 font-bold">Adminístralos</span>
        </p>

        <Alerta v-if="alerta.mensaje" :alerta="alerta" />

        <form class="bg-gray-600 shadow-md rounded-lg py-10 px-5 mb-10" @submit.prevent="validar">
            <div class="mb-5">
                <label for="mascota" class="block  uppercase font-bold">Nombre de Mascota</label>
                <input type="text" id="mascota"
                    class="border-2 border-gray-500 focus:border-gray-600 w-full p-2 mt-2 placeholder-gray-400 rounded-md bg-gray-700 text-gray-200"
                    placeholder="Scrapy" :value="nombre" @input="$emit('update:nombre', $event.target.value)">
            </div>

            <div class="mb-5">
                <label for="propietario" class="block  uppercase font-bold">Propietario</label>
                <input type="text" id="propietario"
                    class="border-2 border-gray-500 focus:border-gray-600 w-full p-2 mt-2 placeholder-gray-400 rounded-md bg-gray-700 text-gray-200"
                    placeholder="María Rodriguez" :value="propietario"
                    @input="$emit('update:propietario', $event.target.value)">
            </div>

            <div class="mb-5">
                <label for="email" class="block  uppercase font-bold">email</label>
                <input type="email" id="email"
                    class="border-2 border-gray-500 focus:border-gray-600 w-full p-2 mt-2 placeholder-gray-400 rounded-md bg-gray-700 text-gray-200"
                    placeholder="propietario@email.com" :value="email"
                    @input="$emit('update:email', $event.target.value)">
            </div>

            <div class="mb-5">
                <label for="alta" class="block  uppercase font-bold">Alta</label>
                <input type="date" id="alta"
                    class="border-2 border-gray-500 focus:border-gray-600 w-full p-2 mt-2 placeholder-gray-400 rounded-md bg-gray-700 text-gray-200"
                    :value="alta" @input="$emit('update:alta', $event.target.value)">
            </div>

            <div class="mb-5">
                <label for="sintomas" class="block  uppercase font-bold">Síntomas</label>
                <textarea type="date" id="sintomas"
                    class="border-2 border-gray-500 focus:border-gray-600 w-full p-2 mt-2 placeholder-gray-400 rounded-md bg-gray-700 text-gray-200 h-32"
                    placeholder="Descripción de los síntomas del paciente" :value="sintomas"
                    @input="$emit('update:sintomas', $event.target.value)" />
            </div>

            <button type="submit"
                class="flex items-center justify-center bg-emerald-500 w-full p-3 text-white uppercase font-bold hover:bg-emerald-600 rounded-md cursor-pointer transition-colors">
                <svg xmlns="http://www.w3.org/2000/svg" class="icon icon-tabler"
                    :class="[editando ? 'icon-tabler-device-floppy' : 'icon-tabler-clipboard-check']" width="22"
                    height="22" viewBox="0 0 24 24" stroke-width="1.5" stroke="#FFFFFF" fill="none"
                    stroke-linecap="round" stroke-linejoin="round">
                    <path stroke="none" d="M0 0h24v24H0z" fill="none" />
                    <path
                        :d="[editando ? 'M6 4h10l4 4v10a2 2 0 0 1 -2 2h-12a2 2 0 0 1 -2 -2v-12a2 2 0 0 1 2 -2' : 'M9 5h-2a2 2 0 0 0 -2 2v12a2 2 0 0 0 2 2h10a2 2 0 0 0 2 -2v-12a2 2 0 0 0 -2 -2h-2']" />
                    <path
                        :d="[editando ? 'M12 14m-2 0a2 2 0 1 0 4 0a2 2 0 1 0 -4 0' : 'M9 3m0 2a2 2 0 0 1 2 -2h2a2 2 0 0 1 2 2v0a2 2 0 0 1 -2 2h-2a2 2 0 0 1 -2 -2z']" />
                    <path :d="[editando ? 'M14 4l0 4l-6 0l0 -4' : 'M9 14l2 2l4 -4']" />
                </svg>


                {{ editando ? 'Guardar Cambios' : 'Registrar Paciente' }}
            </button>
        </form>
    </div>
</template>

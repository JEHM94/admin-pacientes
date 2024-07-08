<script setup>
defineEmits(['actualizar-paciente', 'eliminar-paciente'])

defineProps({
    paciente: {
        type: Object,
        required: true
    }
})
</script>

<template>
    <div class="mx-5 mb-10 bg-gray-600 shadow-md p-5 rounded-xl">
        <p class="font-bold mb-3 ">ID:
            <span class="font-normal normal-case">
                {{ paciente.id }}
            </span>
        </p>

        <p class="font-bold mb-3 ">Nombre:
            <span class="font-normal normal-case">
                {{ paciente.nombre }}
            </span>
        </p>

        <p class="font-bold mb-3 ">Propietario:
            <span class="font-normal normal-case">
                {{ paciente.propietario }}
            </span>
        </p>

        <p class="font-bold mb-3 ">Email:
            <span class="font-normal normal-case">
                {{ paciente.email }}
            </span>
        </p>

        <p class="font-bold mb-3 ">Fecha Alta:
            <span class="font-normal normal-case">
                {{ paciente.alta }}
            </span>
        </p>

        <p class="font-bold mb-3 ">Síntomas:
            <span class="font-normal normal-case">
                {{ paciente.sintomas }}
            </span>
        </p>

        <div class="grid md:grid-cols-2  gap-5 mt-10 ">
            <button type="button" @click="$emit('actualizar-paciente', paciente.id)"
                class="flex items-center justify-center gap1 w-full py-2 px-10 bg-[#2196f3] hover:bg-[#1976d2] text-white font-bold  rounded-lg">
                <svg xmlns="http://www.w3.org/2000/svg" class="icon icon-tabler icon-tabler-file-description" width="20"
                    height="20" viewBox="0 0 24 24" stroke-width="1.5" stroke="#FFFFFF" fill="none"
                    stroke-linecap="round" stroke-linejoin="round">
                    <path stroke="none" d="M0 0h24v24H0z" fill="none" />
                    <path d="M14 3v4a1 1 0 0 0 1 1h4" />
                    <path d="M17 21h-10a2 2 0 0 1 -2 -2v-14a2 2 0 0 1 2 -2h7l5 5v11a2 2 0 0 1 -2 2z" />
                    <path d="M9 17h6" />
                    <path d="M9 13h6" />
                </svg>
                Editar
            </button>

            <button type="button" @click="$emit('eliminar-paciente', paciente.id)"
                class="flex items-center justify-center w-full py-2 px-10 bg-[#f44336] hover:bg-[#d32f2f] text-white font-bold  rounded-lg">
                <svg xmlns="http://www.w3.org/2000/svg" class="icon icon-tabler icon-tabler-playlist-x" width="26"
                    height="26" viewBox="0 0 24 24" stroke-width="1.5" stroke="#FFFFFF" fill="none"
                    stroke-linecap="round" stroke-linejoin="round">
                    <path stroke="none" d="M0 0h24v24H0z" fill="none" />
                    <path d="M19 8h-14" />
                    <path d="M5 12h7" />
                    <path d="M12 16h-7" />
                    <path d="M16 14l4 4" />
                    <path d="M20 14l-4 4" />
                </svg>
                Eliminar
            </button>
        </div>
    </div>
</template>
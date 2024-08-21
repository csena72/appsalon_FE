<script setup>
import VueTailwindDatepicker from  'vue-tailwind-datepicker'
import { formatCurrency } from '@/helpers'
import SelectedService from '@/components/SelectedService.vue';
import { useAppointmentsStore } from '@/stores/appointments';

const appointments = useAppointmentsStore()

</script>

<template>
    <h2 class="text-4xl font-extrabold text-white">Detalles de Cita y Resumen</h2>
    <p class="text-white text-lg">A continuación verifica tu información y confirma tu cita</p>

    <h3 class="text-3xl font-extrabold text-white">Servicios</h3>

    <p v-if="appointments.noServicesSelected" class="text-white text-2xl text-center">No hay servicios seleccionados.</p>
    <div v-else class="grid gap-5">
        <SelectedService
            v-for="service in appointments.services"
            :key="service._id"
            :service="service"
        />
        <p class="text-right text-2xl text-white">Total a pagar: 
            <span class="font-black">
                {{ formatCurrency(appointments.totalAmount) }}
            </span>
        </p>
    </div>
    
    <div class="space-y-8" v-if="!appointments.noServicesSelected">
        <h3 class="text-3xl font-extrabold text-white">Fecha y Hora</h3>

        <div class="lg:flex gap-5 items-start">
            <div class="w-full lg:w-96 bg-white flex justify-center rounded-lg">

                <VueTailwindDatepicker
                    i18n="es"
                    as-single
                    no-input
                />
            </div>
            <div>

            </div>
        </div>
    </div>

</template>



<script setup>
import { ref, reactive } from 'vue';
import Header from './components/Header.vue'
import Form from './components/Form.vue'
import Patient from './components/Patient.vue'

const patients = ref([])

const patient = reactive({
  name: '',
  owner: '',
  email: '',
  clearanceDate: '',
  symptoms: ''
})

const savePatient = () => {
  patients.value.push({ ...patient })
  patient.name = ''
  patient.owner = ''
  patient.email = ''
  patient.clearanceDate = ''
  patient.symptoms = ''
}
</script>

<template>
  <div class="container mx-auto mt-20 px-4">
    <Header />
    <div class="mt-12 md:flex">
      <Form v-model:name="patient.name" v-model:owner="patient.owner" v-model:email="patient.email"
        v-model:clearanceDate="patient.clearanceDate" v-model:symptoms="patient.symptoms" @save-patient="savePatient" />
      <div class="md:w-1/2 md:h-screen overflow-y-scroll">
        <h3 class="font-black text-3xl text-center">Check your patients</h3>

        <div v-if="patients.length > 0">
          <p class="text-lg mt-5 text-center mb-10">
            Patients
            <span class="text-indigo-600 font-bold">Information</span>
          </p>
          <Patient v-for="patient in patients" :patient="patient" />
        </div>
        <p v-else class="mt-20 text-2xl text-center">There aren't patients</p>
      </div>
    </div>
  </div>
</template>


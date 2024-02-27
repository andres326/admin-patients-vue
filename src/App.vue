<script setup>
import { ref, reactive, watch, onMounted } from 'vue';
import { uid } from 'uid'
import Header from './components/Header.vue'
import Form from './components/Form.vue'
import Patient from './components/Patient.vue'

const patients = ref([])

const patient = reactive({
  id: null,
  name: '',
  owner: '',
  email: '',
  clearanceDate: '',
  symptoms: ''
})

watch(patients, () => {
  savePatientsToStorage()
}, {
  deep: true
})

onMounted(() => {
  const storagedPatients = localStorage.getItem('patients')
  if (storagedPatients) {
    patients.value = JSON.parse(storagedPatients)
  }
})

const savePatientsToStorage = () => {
  localStorage.setItem('patients', JSON.stringify(patients.value))
}

const savePatient = () => {
  if (patient.id) {
    const { id } = patient
    const index = patients.value.findIndex(patient => patient.id === id)
    patients.value[index] = { ...patient }
  } else {
    patients.value.push({ ...patient, id: uid() })
  }
  patient.id = null
  patient.name = ''
  patient.owner = ''
  patient.email = ''
  patient.clearanceDate = ''
  patient.symptoms = ''
}

const updatePatient = (id) => {
  const patientEdit = patients.value.filter(patient => patient.id === id)[0]
  Object.assign(patient, patientEdit)
}

const deletePatient = id => {
  patients.value = patients.value.filter(patient => patient.id !== id)
}
</script>

<template>
  <div class="container mx-auto mt-20 px-4">
    <Header />
    <div class="mt-12 md:flex">
      <Form v-model:name="patient.name" v-model:owner="patient.owner" v-model:email="patient.email"
        v-model:clearanceDate="patient.clearanceDate" v-model:symptoms="patient.symptoms" @save-patient="savePatient"
        :id="patient.id" />
      <div class="md:w-1/2 md:h-screen overflow-y-scroll">
        <h3 class="font-black text-3xl text-center">Check your patients</h3>

        <div v-if="patients.length > 0">
          <p class="text-lg mt-5 text-center mb-10">
            Patients
            <span class="text-indigo-600 font-bold">Information</span>
          </p>
          <Patient v-for="patient in patients" :patient="patient" @update-patient="updatePatient"
            @delete-patient="deletePatient" />
        </div>
        <p v-else class="mt-20 text-2xl text-center">There aren't patients</p>
      </div>
    </div>
  </div>
</template>


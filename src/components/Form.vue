<script setup>
import { reactive } from 'vue';
import Alert from './Alert.vue'

const alert = reactive({
  type: '',
  message: ''
})

const patient = reactive({
  name: '',
  owner: '',
  email: '',
  clearanceDate: '',
  symptoms: ''
})

const onSubmit = () => {
  if (Object.values(patient).includes('')) {
    alert.message = 'All fields are required'
    alert.type = 'error'
    return
  }
}
</script>

<template>
  <div class="md:w-1/2">
    <h2 class="font-black text-3xl text-center">Monitoring</h2>
    <p class="text-lg mt-5 text-center mb-10">
      Add patients and
      <span class="text-indigo-600 font-bold">monitoring them</span>
    </p>

    <Alert v-if="alert.message" :alert="alert" />
    <form class="bg-white shadow-md rounded-lg py-10 px-5 mb-10" @submit.prevent="onSubmit">
      <div class="mb-5">
        <label class="block text-gray-700 uppercase font-bold" for="pet">Pet Name</label>
        <input id="pet" type="text" placeholder="Pet" class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md"
          v-model="patient.name" />
      </div>
      <div class="mb-5">
        <label class="block text-gray-700 uppercase font-bold" for="owner">Owner's Name</label>
        <input id="owner" type="text" placeholder="Owner" class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md"
          v-model="patient.owner" />
      </div>
      <div class="mb-5">
        <label class="block text-gray-700 uppercase font-bold" for="email">Email</label>
        <input id="email" type="email" placeholder="Owner's email"
          class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md" v-model="patient.email" />
      </div>
      <div class="mb-5">
        <label class="block text-gray-700 uppercase font-bold" for="clearance">Medical Clearance</label>
        <input id="cleareance" type="date" class="border-2 w-full p-2 mt-2 rounded-md" v-model="patient.clearanceDate" />
      </div>
      <div class="mb-5">
        <label class="block text-gray-700 uppercase font-bold" for="symptoms">Symptoms</label>
        <textarea id="symptoms" placeholder="Describe the symptoms"
          class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md h-32" v-model="patient.symptoms" />
      </div>
      <input type="submit"
        class="bg-indigo-600 w-full p-3 text-white uppercase font-bold hover:bg-indigo-700 cursor-pointer transition-colors"
        value="Register Patient" />
    </form>
  </div>
</template>


<script setup>
import { reactive, computed } from 'vue';
import Alert from './Alert.vue'

const emit = defineEmits(['update:name', 'update:owner', 'update:email', 'update:clearanceDate', 'update:symptoms', 'save-patient'])

const props = defineProps({
  id: {
    type: [String, null],
    required: true
  },
  name: {
    type: String,
    required: true
  },
  owner: {
    type: String,
    required: true
  },
  email: {
    type: String,
    required: true
  },
  clearanceDate: {
    type: String,
    required: true
  },
  symptoms: {
    type: String,
    required: true
  }
})

const alert = reactive({
  type: '',
  message: ''
})

const onSubmit = () => {
  if (Object.values(props).includes('')) {
    alert.message = 'All fields are required'
    alert.type = 'error'
    return
  }

  emit('save-patient')
  alert.message = 'Patient saved succesfully'
  alert.type = 'success'

  setTimeout(() => {
    Object.assign(alert, {
      type: '',
      message: ''
    })
  }, 3000)
}

const editing = computed(() => props.id)
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
          @input="$emit('update:name', $event.target.value)" :value="name" />
      </div>
      <div class="mb-5">
        <label class="block text-gray-700 uppercase font-bold" for="owner">Owner's Name</label>
        <input id="owner" type="text" placeholder="Owner" class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md"
          @input="$emit('update:owner', $event.target.value)" :value="owner" />
      </div>
      <div class="mb-5">
        <label class="block text-gray-700 uppercase font-bold" for="email">Email</label>
        <input id="email" type="email" placeholder="Owner's email"
          class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md"
          @input="$emit('update:email', $event.target.value)" :value="email" />
      </div>
      <div class="mb-5">
        <label class="block text-gray-700 uppercase font-bold" for="clearance">Medical Clearance</label>
        <input id="cleareance" type="date" class="border-2 w-full p-2 mt-2 rounded-md"
          @input="$emit('update:clearanceDate', $event.target.value)" :value="clearanceDate" />
      </div>
      <div class="mb-5">
        <label class="block text-gray-700 uppercase font-bold" for="symptoms">Symptoms</label>
        <textarea id="symptoms" placeholder="Describe the symptoms"
          class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md h-32"
          @input="$emit('update:symptoms', $event.target.value)" :value="symptoms" />
      </div>
      <input type="submit"
        class="bg-indigo-600 w-full p-3 text-white uppercase font-bold hover:bg-indigo-700 cursor-pointer transition-colors"
        :value="[editing ? 'Save Patient' : 'Register Patient']" />
    </form>
  </div>
</template>


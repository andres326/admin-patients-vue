<script setup>
import { ref } from 'vue';
import Header from './components/Header.vue'
import Form from './components/Form.vue'

const patients = ref([])
</script>

<template>
  <div class="container mx-auto mt-20 px-4">
    <Header />
    <div class="mt-12 md:flex">
      <Form />
      <div class="md:w-1/2 md:h-screen overflow-y-scroll">
        <h3 class="font-black text-3xl text-center">Check your patients</h3>

        <div v-if="patients.length > 0"></div>
        <p v-else class="mt-20 text-2xl text-center">There aren't patients</p>
      </div>
    </div>
  </div>
</template>


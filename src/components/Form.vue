<script setup>
  import { reactive } from 'vue';
  import Alert from './Alert.vue';

  const alert = reactive({
    description: '',
    type: ''
  })

  const patient = reactive({
    name: '',
    owner: '',
    email: '',
    discharge: '',
    symptoms: ''
  })
  
  const validateForm = () => {
    if (Object.values(patient).includes('')){
      alert.description = 'All fields are required';
      alert.type = 'error';
      return;
    }


  }

</script>

<template>
  <div class="md:w-1/2">
    <h2 class="font-black text-3xl text-center">Seguimiento pacientes</h2>
    
    <p class="text-lg mt-5 text-center mb-10">
      Añade Pacientes y 
      <span class="text-indigo-600 font-bold">Administralos</span>
    </p>

    <Alert 
      :alert="alert"
    />
    <form 
      class="bg-white shadow-md rounded-lg py-10 px-5 mb-10"
      @submit.prevent="validateForm"
      > 
      <div class="mb-5">
        <label for="pet"
          class="block text-gray-700 uppercase font-bold"
        >
          Name of the pet
        </label>

        <input 
          id="pet"
          type="text"
          placeholder="Name of the pet"
          v-model="patient.name"
          class="border-2 w-full mt-2 p-2 placeholder-gray-400 rounded-md"
        >
      </div>

      <div class="mb-5">
        <label for="owner"
          class="block text-gray-700 uppercase font-bold"
        >
          Name of the owner
        </label>

        <input 
          id="owner"
          type="text"
          placeholder="Name of the owner"
          class="border-2 w-full mt-2 p-2 placeholder-gray-400 rounded-md"
          v-model="patient.owner"
        >
      </div>


      <div class="mb-5">
        <label for="email"
          class="block text-gray-700 uppercase font-bold"
        >
          Owner Email
        </label>

        <input 
          id="email"
          type="email"
          placeholder="Email"
          class="border-2 w-full mt-2 p-2 placeholder-gray-400 rounded-md"
          v-model="patient.email"
        >
      </div>


      <div class="mb-5">
        <label for="discharge"
          class="block text-gray-700 uppercase font-bold"
        >
          Discharge
        </label>

        <input 
          id="discharge"
          type="date"
          placeholder="Discharge"
          class="border-2 w-full mt-2 p-2 placeholder-gray-400 rounded-md"
          v-model="patient.discharge"
        >
      </div>

      <div class="mb-5">
        <label for="Symptoms"
          class="block text-gray-700 uppercase font-bold"
        >
          Symptoms
        </label>

        <textarea 
          id="Symptoms"
          placeholder="Describe the symptoms"
          class="border-2 w-full mt-2 p-2 placeholder-gray-400 rounded-md h-40"
          v-model="patient.symptoms"
        />
      </div>

      <input 
        type="submit"
        class="bg-indigo-600 w-full p-3 text-white uppercase font-bold hover:bg-indigo-700 cursor-pointer transition-colors"
        value="Add patient"
        />
    </form>


  </div>
</template>

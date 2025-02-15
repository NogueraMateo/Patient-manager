<script setup>
  import { reactive } from 'vue';
  import Alert from './Alert.vue';

  const alert = reactive({
    description: '',
    type: ''
  })

  const props = defineProps({
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
    discharge: {
      type: String,
      required: true
    },
    symptoms: {
      type: String,
      required: true
    }
  })

  const emit = defineEmits(['update:name', 'update:owner', 'update:email', 'update:discharge', 'update:symptoms', 'add-patient'])
  
  const validateForm = () => {
    if (Object.values(props).includes('')){
      alert.description = 'All fields are required';
      alert.type = 'error';
      return;
    }

    emit('add-patient')
    alert.description = 'Patient added successfully';
    alert.type = 'success';

    setTimeout(() => {
      Object.assign(alert, {
        description: '',
        type: ''
      })
    }, 3000)

  }

</script>

<template>
  <div class="md:w-1/2">
    <h2 class="font-black text-3xl text-center">
      Patient tracking
    </h2>
    
    <p class="text-lg mt-5 text-center mb-10">
      Add patients and
      <span class="text-indigo-600 font-bold">manage them</span>
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
          class="border-2 w-full mt-2 p-2 placeholder-gray-400 rounded-md"
          :value="name"
          @input="$emit('update:name', $event.target.value)"
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
          :value="owner" 
          @input="$emit('update:owner', $event.target.value)"
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
          :value="email"
          @input="$emit('update:email', $event.target.value)"
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
          :value="discharge"
          @input="$emit('update:discharge', $event.target.value)"

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
          :value="symptoms"
          @input="$emit('update:symptoms', $event.target.value)"
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

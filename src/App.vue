<script setup>

  import { ref, reactive, onMounted, watch } from 'vue';
  import { uid } from 'uid';
  import Header from './components/Header.vue';
  import Form from './components/Form.vue';
  import Patient from './components/Patient.vue';

  const patients = ref([]);

  const patient = reactive({
    id: null,
    name: '',
    owner: '',
    email: '',
    discharge: '',
    symptoms: ''
  })

  watch(patients, () => {
    addPatientLocalStorage()
  } , { deep: true })

  onMounted(() => {
    const patientsLocalStorage = localStorage.getItem('patients')

    if (patientsLocalStorage) {
      patients.value = JSON.parse(patientsLocalStorage)
    }
  })

  const addPatient = () => {
    patients.value.push({...patient, id: uid()})

    // Reset form
    Object.assign(patient, {
      name: '',
      owner: '',
      email: '',
      discharge: '',
      symptoms: ''
    })

 }

  const deletePatient = (id) => {
    patients.value = patients.value.filter(p => p.id !== id)

  }

  const addPatientLocalStorage = () => {
    localStorage.setItem('patients', JSON.stringify(patients.value))
  }

</script>

<template>
  <div class="container mx-auto mt-20">
    <Header />

    <div class="mt-12 md:flex">
      <Form 
        v-model:name="patient.name"
        v-model:owner="patient.owner"
        v-model:email="patient.email"
        v-model:discharge="patient.discharge"
        v-model:symptoms="patient.symptoms"
        @add-patient="addPatient"
      />

      <div 
        class="md:w-1/2 md:h-screen overflow-y-scroll"
      >
        <h3 class="font-black text-3xl text-center">
          Manage your patients
        </h3>

        <p class="text-lg mt-5 text-center mb-10">
          <span class="text-indigo-600 font-bold">Patients</span>
          information
        </p>
            
        <div
          v-if="patients.length > 0"
        >
          <Patient
            v-for="p in patients"
            :patient="p"
            @delete-patient="deletePatient"
          />

        </div>

        <p 
          v-else
          class="text-center mt-20 text-2xl"
          >
          No patients registered
        </p>

      </div>

     </div>
  </div>
</template>
<script setup>

  import { computed } from 'vue';

  const props = defineProps({
    alert: {
      type: Object,
      required: true
    }
  })

  const isError = computed(() => {
    return props.alert.type === 'error';
  }
  )

</script>

<template>
  <div
    v-if="alert.description"
    :class="[isError ? 'bg-red-500' : 'bg-green-500']"
    class="p-3 mb-3 text-center font-bold uppercase text-white rounded-md"
  >
    {{ alert.description }}
  </div>
</template>


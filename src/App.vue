<template>
  <div class="p-4">
    <div class="text-center mb-6 bg-indigo-50 p-4 rounded-lg shadow-md">
      <fileUploader @loadFacturae="loadFacturae" />
    </div>
    <div v-if="loading" class="flex justify-center items-center h-screen">
      <div class="rounded-full h-20 w-20 bg-violet-800 animate-ping"></div>
    </div>
    <div v-if="loaded">
      <Invoice :invoice="invoice" />
    </div>
  </div>
  
</template>

<script setup>
import { onMounted, ref } from "vue";
import fileUploader from "./components/fileUploader.vue";
import Invoice from "./components/invoice.vue";
const loading = ref(false);
const loaded = ref(false)
const invoice = ref(null);
onMounted(() => {});
const loadFacturae = (facturae) => {
  loading.value = true;
  setTimeout(() => {
    invoice.value = facturae ;
    loading.value = false
    loaded.value = true
  }, 1400);
  console.log(facturae);
};
</script>

<style scoped></style>

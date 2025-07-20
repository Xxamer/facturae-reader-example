<template>
  <div
    class="border-2 border-dashed border-gray-300 rounded-md p-6 text-center hover:border-gray-400 transition-colors max-w-[60%] mx-auto"
    @dragover.prevent
    @drop.prevent="handleDrop"
    :class="{ 'border-blue-500 bg-blue-50': isDragging }"
    @dragenter.prevent="isDragging = true"
    @dragleave.prevent="isDragging = false"
  >
    <p class="mb-2 text-gray-600">Drop your files here</p>
    <input
      class="border border-gray-300 rounded-md text-center p-2"
      type="file"
      id="input"
      @change="handleFile($event)"
    />
  </div>
</template>

<script lang="ts" setup>
import { readFacturae } from "facturaereader";
import { onMounted, ref, defineEmits } from "vue";

const emit = defineEmits(["loadFacturae"]);
const isDragging = ref(false);

onMounted(() => {});

const handleFile = async (event: any) => {
  const file = event.target.files[0];
  await processFile(file);
  event.target.value = "";
};

const handleDrop = async (event: DragEvent) => {
  isDragging.value = false;
  const file = event.dataTransfer?.files[0];
  if (file) {
    await processFile(file);
  }
};

const processFile = async (file: File) => {
  const data = await readFacturae(file);
  emit("loadFacturae", data);
  console.log(data);
};
</script>

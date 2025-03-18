<script setup>
import { ref } from 'vue';

const title = "TODO LIST VUE.JS";
const newTask = ref('');
const tasks = ref([]);
const error = ref(false);

const addTask = () => {
  if (newTask.value.trim() === '') {
    error.value = true;
    return;
  }
  tasks.value.push(newTask.value);
  newTask.value = '';
  error.value = false;
};

const removeTask = (index) => {
  tasks.value = tasks.value.filter((task, i) => i !== index);
  // tasks.value.splice(index, 1);
};
</script>

<template>
  <div class="flex flex-col justify-center items-center min-h-screen bg-[#f5f5f5] p-3">
    <div class="max-w-md w-full p-4 bg-white rounded-2xl shadow-lg text-center">
      <img src="./../assets/logo.svg" alt="Logo Vue.js" class="w-16 h-16 m-auto my-3" />
      <h1 class="text-xl font-bold mb-4">{{ title }}</h1>
      <div class="flex flex-col items-center gap-2 mb-4">
        <input v-model="newTask" @keyup.enter="addTask" type="text" placeholder="Tambah tugas..."
          :class="{ 'border-red-500 focus:ring-1 focus:ring-red-500': error, 'border-gray-300 focus:ring-blue-500': !error }"
          class="w-full px-3 py-2 border rounded-lg focus:outline-none" />
        <small v-if="error" class="text-red-500">Tugas tidak boleh kosong</small>
        <button @click="addTask"
          class="bg-blue-500 hover:bg-blue-600 text-white px-4 py-2 rounded-lg w-full">Tambah</button>
      </div>
      <div class="flex flex-col items-center" v-if="tasks.length">
        <div v-for="(task, index) in tasks" :key="index"
          class="flex justify-between items-center w-full p-3 mb-2 shadow-md border rounded-lg">
          <span class="ps-2 text-start">{{ task }}</span>
          <button @click="removeTask(index)" class="text-red-500" aria-label="Delete">
            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5"
              stroke="currentColor" class="size-6">
              <path stroke-linecap="round" stroke-linejoin="round"
                d="M12 9.75 14.25 12m0 0 2.25 2.25M14.25 12l2.25-2.25M14.25 12 12 14.25m-2.58 4.92-6.374-6.375a1.125 1.125 0 0 1 0-1.59L9.42 4.83c.21-.211.497-.33.795-.33H19.5a2.25 2.25 0 0 1 2.25 2.25v10.5a2.25 2.25 0 0 1-2.25 2.25h-9.284c-.298 0-.585-.119-.795-.33Z" />
            </svg>
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

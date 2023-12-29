<script setup>
import { ref, onMounted } from "vue";

const data = ref([]);

const getData = async () => {
  try {
    const res = await fetch("http://localhost:3000/peoples");
    if (!res.ok) {
      throw new Error(`HTTP error! Status: ${res.status}`);
    }
    data.value = await res.json();
    console.log(data.value);
  } catch (error) {
    console.log(error);
  }
};

onMounted(() => {
  getData();
});
</script>

<template>
  <div class="bg-gray-100">
    <div class="container mx-auto p-4">
      <!-- Header -->
      <div class="flex justify-between items-center mb-4">
        <h1 class="text-2xl font-bold">Data List</h1>
        <div class="flex space-x-2">
          <input
            type="text"
            placeholder="Search..."
            class="border p-2 rounded"
          />
          <button class="bg-blue-500 text-white px-4 py-2 rounded">
            Search
          </button>
          <button class="bg-green-500 text-white px-4 py-2 rounded">
            Add New Data
          </button>
        </div>
      </div>

      <!-- Table -->
      <table class="w-full border">
        <thead>
          <tr class="bg-gray-200">
            <th class="border p-2">ID</th>
            <th class="border p-2">Name</th>
            <th class="border p-2">Place</th>
            <!-- Add more table headers as needed -->
          </tr>
        </thead>
        <tbody>
          <tr v-for="item in data" :key="item.id">
            <td class="border p-2">{{ item.id }}</td>
            <td class="border p-2">{{ item.name }}</td>
            <td class="border p-2">{{ item.address }}</td>
            <!-- Add more table data as needed -->
          </tr>
          <!-- Add more table rows as needed -->
        </tbody>
      </table>
    </div>
  </div>
</template>

<style scoped></style>

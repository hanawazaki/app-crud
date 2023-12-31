<script setup>
import { ref, onMounted } from "vue";
import CreateModal from "./components/CreateModal.vue";
import EditModal from "./components/EditModal.vue";

const data = ref([]);
const createModal = ref(false);

const showCreateModal = () => {
  createModal.value = !createModal.value;
};

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
  <div class="bg-[#fafafa] min-h-screen">
    <div class="max-w-6xl p-10 mx-auto">
      <div class="m-auto bg-white p-7 rounded-lg shadow-md">
        <!-- Header -->
        <div class="flex justify-between items-center mb-4">
          <h1 class="text-2xl font-bold">Data List</h1>
          <div class="flex space-x-2">
            <input
              type="text"
              placeholder="Search..."
              class="input input-sm input-bordered w-full max-w-xs"
            />
            <button class="btn btn-outline btn-sm" @click="showCreateModal">
              <svg
                xmlns="http://www.w3.org/2000/svg"
                fill="none"
                viewBox="0 0 24 24"
                stroke-width="1.5"
                stroke="currentColor"
                class="w-6 h-6"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  d="M12 9v6m3-3H9m12 0a9 9 0 1 1-18 0 9 9 0 0 1 18 0Z"
                />
              </svg>
              New Data
            </button>
            <CreateModal
              :createModal="createModal"
              @modalshow="showCreateModal"
            />
          </div>
        </div>

        <!-- Table -->
        <div class="overflow-x-auto">
          <table class="table">
            <!-- head -->
            <thead>
              <tr>
                <th>Name</th>
                <th>Email</th>
                <th>Phone</th>
                <th>Gender</th>
                <th>Action</th>
              </tr>
            </thead>
            <tbody>
              <!-- row 1 -->
              <tr v-for="item in data" :key="item.id">
                <td>
                  <div class="flex items-center gap-3">
                    <div class="avatar">
                      <div class="mask mask-squircle w-12 h-12">
                        <img
                          src="https://daisyui.com/tailwind-css-component-profile-2@56w.png"
                          alt="Avatar Tailwind CSS Component"
                        />
                      </div>
                    </div>
                    <div>
                      <div class="font-bold">{{ item.name }}</div>
                      <div class="text-sm opacity-50">{{ item.city }}</div>
                    </div>
                  </div>
                </td>
                <td>
                  {{ item.email }}
                </td>
                <td>{{ item.phone }}</td>
                <td>{{ item.gender }}</td>
                <td class="">
                  <button class="btn btn-info btn-xs mr-2">View</button>
                  <button
                    class="btn btn-success btn-xs mr-2"
                    onclick="my_modal_2.showModal()"
                  >
                    Edit
                  </button>

                  <button class="btn btn-error btn-xs">Delete</button>
                </td>
              </tr>
            </tbody>
          </table>
          <EditModal />
        </div>
        <!--  -->
        <div class="flex justify-center my-5">
          <div class="join">
            <button class="join-item btn">1</button>
            <button class="join-item btn btn-active">2</button>
            <button class="join-item btn">3</button>
            <button class="join-item btn">4</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped></style>

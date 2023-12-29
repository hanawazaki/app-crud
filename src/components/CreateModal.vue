<template>
  <dialog id="my_modal_1" class="modal">
    <div class="modal-box max-w-[600px]">
      <div class="flex justify-between">
        <h3 class="font-bold text-lg">Tambah Data Baru</h3>
        <form method="dialog">
          <button class="btn btn-circle btn-outline btn-sm">
            <svg
              xmlns="http://www.w3.org/2000/svg"
              class="h-6 w-6"
              fill="none"
              viewBox="0 0 24 24"
              stroke="currentColor"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M6 18L18 6M6 6l12 12"
              />
            </svg>
          </button>
        </form>
      </div>
      <form @submit.prevent="handleSubmit">
        <div class="flex gap-3 justify-between">
          <!-- name -->
          <Input
            name="Nama"
            class=""
            placeholder="isi nama"
            type="text"
            v-model="name"
          />
          <!-- email -->
          <Input
            name="Email"
            class=""
            placeholder="isi email"
            type="email"
            v-model="email"
          />
        </div>
        <div class="flex gap-3 justify-between">
          <!-- ttl -->
          <Input
            name="Tempat lahir"
            class=""
            placeholder="isi tempat lahir"
            type="text"
          />
          <Input
            name="Tanggal lahir"
            class=""
            placeholder="isi tanggal lahir"
            type="text"
          />
        </div>
        <div class="flex gap-3 justify-between">
          <!-- religion -->
          <SelectInput
            name="Religion"
            class=""
            v-model="religion"
            :options="selectOptions"
          >
          </SelectInput>
          <!-- gender -->
          <Input
            name="Gender"
            class=""
            placeholder="isi gender"
            type="text"
            v-model="gender"
          />
        </div>
        <div class="flex gap-3 justify-between">
          <!-- notelp -->
          <Input
            name="No Telp"
            class=""
            placeholder="isi no telp"
            type="text"
            v-model="notelp"
          />
          <!-- city -->
          <Input
            name="Kota"
            class=""
            placeholder="isi kota"
            type="text"
            v-model="city"
          />
        </div>
        <!-- alamat -->
        <Input
          name="Alamat"
          class=""
          placeholder="isi alamat"
          type="textarea"
          v-model="address"
        />
        <div class="flex gap-2">
          <button class="btn btn-error">Cancel</button>
          <button class="btn btn-primary">Save</button>
        </div>
      </form>
    </div>
  </dialog>
</template>

<script setup>
import Input from "./Input.vue";
import SelectInput from "./SelectInput.vue";
import { ref } from "vue";

const props = defineProps({
  showModalCreate: {
    type: Boolean,
  },
});

const selectOptions = ref(["Islam", "Kristen", "Protestan", "Hindu", "Budha"]);

console.log(props.showModalCreate);
</script>

<style lang="scss" scoped></style>

<template>
  <dialog class="modal" :class="{ 'modal-open': createModal }">
    <div class="modal-box max-w-[600px]">
      <div class="flex justify-between">
        <h3 class="font-bold text-lg">Tambah Data Baru</h3>
        <form method="dialog">
          <button class="btn btn-circle btn-outline btn-sm" @click="closeModal">
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
          <InputText
            type="text"
            label="Nama"
            placeholder="isi nama"
            v-model="formData.name"
            :isError="hasErrors"
          />

          <!-- email -->
          <InputText
            type="email"
            label="Email"
            placeholder="isi email"
            v-model="formData.email"
            :isError="hasErrors"
          />
        </div>
        <div class="flex gap-3 justify-between">
          <!-- religion -->
          <SelectInput
            label="Agama"
            :options="selectOptions"
            v-model="formData.religion"
          />
          <!-- gender -->
          <CustomRadioInput label="Gender" v-model="formData.gender" />
        </div>
        <div class="flex gap-3 justify-between">
          <!-- notelp -->
          <InputText
            type="text"
            label="No Telepon"
            placeholder="isi no telepon"
            v-model="formData.notelp"
          />
          <!-- city -->
          <InputText
            type="text"
            label="Kota Asal"
            placeholder="isi nama kota"
            v-model="formData.city"
          />
        </div>
        <!-- alamat -->
        <div class="flex gap-2 justify-end">
          <button type="button" @click="resetForm">resetForm</button>
          <button
            type="submit"
            v-if="!isSubmitted"
            class="btn btn-primary w-32"
          >
            Simpan
          </button>
          <button type="button" v-else class="btn btn-primary w-32">
            <Loader />
          </button>
        </div>
      </form>
    </div>
  </dialog>
</template>

<script setup>
import { ref } from "vue";
import InputText from "./InputText.vue";
import SelectInput from "./SelectInput.vue";

import Loader from "./Loader.vue";
import CustomRadioInput from "./CustomRadioInput.vue";

const emits = defineEmits();

const props = defineProps({
  createModal: {
    type: Boolean,
  },
});

const formData = ref({
  name: "",
  email: "",
  notelp: "",
  gender: "",
  religion: "",
  city: "",
});

const isSubmitted = ref(false);
const errors = ref([]);
const hasErrors = ref(false);
const modalShow = ref(props.createModal);

const validateForm = () => {
  errors.value = [];

  if (!formData.value.name.trim()) {
    errors.value.push("Nama tidak boleh kosong");
  }

  const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
  if (!emailRegex.test(formData.value.email)) {
    errors.value.push("Email tidak valid");
  }

  if (!formData.value.religion) {
    errors.value.push("Agama harus dipilih");
  }

  if (!formData.value.gender) {
    errors.value.push("Gender harus dipilih");
  }

  if (!formData.value.notelp.trim()) {
    errors.value.push("Nomor telepon tidak boleh kosong");
  }

  if (!formData.value.city.trim()) {
    errors.value.push("Kota tidak boleh kosong");
  }

  hasErrors.value = errors.value.length > 0;
};

const closeModal = () => {
  emits("modalshow", (modalShow.value = false));
};

const resetForm = () => {
  formData.value.name = "";
  formData.value.email = "";
  formData.value.religion = "";
  formData.value.notelp = "";
  formData.value.city = "";
  formData.value.gender = "";
};

const handleSubmit = () => {
  try {
    // validateForm();

    let data = {
      name: formData.value.name,
      email: formData.value.email,
      notelp: formData.value.notelp,
      gender: formData.value.gender,
      religion: formData.value.religion,
      city: formData.value.city,
    };
    if (hasErrors.value) {
      return;
    }

    isSubmitted.value = true;

    setTimeout(() => {
      fetch("http://localhost:3000/peoples", {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify(data),
      });

      console.log(formData);

      isSubmitted.value = false;

      formData.value.name = "";
      formData.value.email = "";
      formData.value.religion = "";
      formData.value.notelp = "";
      formData.value.city = "";
      formData.value.gender = "";
      closeModal();
    }, 2000);
  } catch (error) {
    console.log(error);
    isSubmitted.value = false;
  }
};

const selectOptions = ref(["Islam", "Kristen", "Katolik", "Hindu", "Budha"]);
</script>

<style scoped>
.error-form {
  background-color: #ffe6e6; /* Warna latar merah */
}
</style>

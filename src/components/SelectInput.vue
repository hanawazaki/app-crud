<template>
  <div class="input-group flex flex-col gap-2 mb-5 w-full">
    <label for="name" class="">{{ name }}</label>
    <select class="select select-bordered w-full max-w-xs">
      <option disabled selected>Pilih Agama</option>
      <option v-for="(option, index) in props.options" :key="index">
        {{ option }}
      </option>
    </select>
  </div>
</template>

<script setup>
const props = defineProps({
  name: {
    type: String,
  },
  value: {
    type: String,
  },
  options: {
    type: Array,
  },
  class: {
    type: String,
  },
});
</script>

<style lang="scss" scoped></style>

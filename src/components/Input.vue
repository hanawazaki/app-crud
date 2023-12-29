<template>
  <!-- textarea -->
  <div
    class="input-group flex flex-col gap-2 mb-5 w-full"
    v-if="type === 'textarea'"
  >
    <label for="name" class="">{{ name }}</label>
    <textarea
      :type="text"
      :placeholder="placeholder"
      class="textarea textarea-bordered"
      :class="class"
      :value="value"
    />
  </div>

  <!-- text -->
  <div class="input-group flex flex-col gap-2 mb-5 w-full" v-else>
    <label for="name" class="">{{ name }}</label>
    <input
      :type="text"
      :placeholder="placeholder"
      class="input input-bordered w-full max-w-xs"
      :class="class"
      :value="value"
    />
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
  type: {
    type: String,
  },
  class: {
    type: String,
  },
  placeholder: {
    type: String,
  },
});
</script>

<style lang="scss" scoped></style>

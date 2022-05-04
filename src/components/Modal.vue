
<template>
  <div
    v-show="modelValue"
    class="
      absolute
      inset-0
      flex
      items-center
      justify-center
      bg-black bg-opacity-50
      shadow-lg
    "
  >
    <div class="max-w-3xl p-6 mx-4 bg-white rounded-sm shadow-xl">
      <div class="flex items-center justify-between">
        <h1 class="text-2xl">{{ title }}</h1>
        <svg
          xmlns="http://www.w3.org/2000/svg"
          class="w-8 h-8 text-red-900 cursor-pointer"
          fill="none"
          @click="$emit('update:modelValue', false)"
          viewBox="0 0 24 24"
          stroke="currentColor"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            stroke-width="2"
            d="M10 14l2-2m0 0l2-2m-2 2l-2-2m2 2l2 2m7-2a9 9 0 11-18 0 9 9 0 0118 0z"
          />
        </svg>
      </div>
      <div class="mt-4">
        <slot></slot>
        <div class="flex justify-between mt-4">
          <button
            @click="$emit('update:modelValue', false)"
            class="px-6 py-2 text-blue-800 border border-blue-600 rounded"
          >
            Cancel
          </button>
          <button
            @click="$emit('addItemToCart', true)"
            class="px-6 py-2 ml-2 text-white bg-primary rounded"
          >
            Add To Cart
          </button>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    title: {
      type: String,
      default: "",
    },
    modelValue: {
      type: Boolean,
      default: false,
    },
  },
};
</script>

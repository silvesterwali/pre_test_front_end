<script setup>
import { ref } from "vue";

defineProps({
  item: {
    type: Object,
    required: true,
  },
});
</script>

<template>
  <div class="relative block bg-white" @click="$emit('addItem', item)">
    <div class="p-1 rounded-lg">
      <img
        loading="lazy"
        :alt="item.name"
        class="object-contain w-full h-56 lg:h-72"
        :src="item.image"
      />
    </div>

    <div class="p-3">
      <h5 class="mt-2 text-medium font-bold text-center truncate">
        {{ item.name }}
      </h5>

      <p class="mt-2 text-sm font-medium text-gray-600 text-center">
        ${{ item.price }}
      </p>
    </div>
  </div>
</template>
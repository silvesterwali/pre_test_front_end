<template>
  <div v-for="(item, index) in toppings" :key="index">
    <label>
      <input type="checkbox" v-model="selectedToppings" />
      {{ item.name }} (${{ item.price }})
    </label>
  </div>
</template>

<script>
export default {
  data() {
    return {
      selectedToppings: [],
    };
  },
  watch: {},
  props: {
    toppings: {
      type: Array,
      required: true,
    },
    modelValue: {
      type: Array,
      default: () => [],
    },
  },
};
</script>
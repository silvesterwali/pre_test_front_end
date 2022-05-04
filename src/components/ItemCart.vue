<template>
  <div class="block" @click="$emit('removeItem', index)">
    <div
      class="
        flex
        items-start
        mt-2
        p-2
        rounded-lg
        shadow-md
        hover:shadow-lg hover:ring-1 hover:ring-secondary
      "
    >
      <img
        class="object-cover w-16 h-20 rounded-sm"
        :src="itemCart.image"
        :alt="itemCart.name"
      />

      <div class="ml-4">
        <h3 class="text-sm">{{ itemCart.name }}</h3>

        <dl class="mt-1 space-y-1 text-xs text-gray-500">
          <div>
            <dt class="inline" v-if="toppingsName.length > 0">
              <span v-for="item in toppingsName" :key="item">{{
                item + ", "
              }}</span>
            </dt>
            <dt class="inline" v-else>No Toppings</dt>
          </div>
          <dt class="inline font-medium">${{ itemCart.total }}</dt>
        </dl>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    itemCart: {
      type: Object,
      required: true,
    },
    index: {
      type: Number,
      required: true,
    },
  },
  computed: {
    toppingsName() {
      return this.itemCart.toppings.map((topping) => topping.name);
    },
  },
};
</script>
<script setup>
import { ref, watch, computed } from "vue";
import Card from "./components/Card.vue";
import Modal from "./components/Modal.vue";
import ToppingFormVue from "./components/ToppingForm.vue";
import ToppingForm from "./components/ToppingForm.vue";
import ItemCartVue from "./components/ItemCart.vue";

const cardItems = ref([]);
const selectedItem = ref(null);
const modal = ref(false);
const addItem = (item) => {
  selectedItem.value = item;
  modal.value = true;
};
const removeItem = (index) => {
  cardItems.value.splice(index, 1);
};
const selectedToppings = ref([]);
const addItemToCart = () => {
  let total = selectedItem.value.price;
  selectedItem.value.toppings = selectedToppings.value;
  if (selectedToppings.value.length > 0) {
    selectedToppings.value.forEach(({ price }) => {
      total += price;
    });
  }
  selectedItem.value.total = total;

  cardItems.value.push(selectedItem.value);
  modal.value = false;
};

let items = ref([
  {
    id: 1,
    image:
      "https://media.istockphoto.com/photos/delicious-vegetarian-pizza-on-white-picture-id1192094401?k=20&m=1192094401&s=612x612&w=0&h=jesvXuPyvqM36GQ5QEvJrL3QZjK6YKsziUUF3ZbW0gw=",
    name: "AMERICAN ClASSIC CHEESEBURGER",
    price: 8,
    toppings: [],
  },
  {
    id: 2,
    image:
      "https://media.istockphoto.com/photos/delicious-vegetarian-pizza-on-white-picture-id1192094401?k=20&m=1192094401&s=612x612&w=0&h=jesvXuPyvqM36GQ5QEvJrL3QZjK6YKsziUUF3ZbW0gw=",
    name: "GRILLED BEEF SUPREME",
    toppings: [],
    price: 12,
  },
  {
    id: 3,
    image:
      "https://media.istockphoto.com/photos/delicious-vegetarian-pizza-on-white-picture-id1192094401?k=20&m=1192094401&s=612x612&w=0&h=jesvXuPyvqM36GQ5QEvJrL3QZjK6YKsziUUF3ZbW0gw=",
    name: "CHEESE MEATBALL BLAST",
    price: 15,
    toppings: [],
  },
]);

let toppings = ref([
  {
    name: "Avocado",
    price: 1,
  },
  {
    name: "Lobster",
    price: 2,
  },
  {
    name: "Bacon",
    price: 3,
  },
  {
    name: "Brocoli",
    price: 1,
  },
  {
    name: "Oyster",
    price: 2,
  },
  {
    name: "Duck",
    price: 3,
  },
  {
    name: "Unions",
    price: 1,
  },

  {
    name: "Salmon",
    price: 2,
  },

  {
    name: "Ham",
    price: 3,
  },
  {
    name: "Zucchini",
    price: 1,
  },

  {
    name: "Tuna",
    price: 2,
  },

  {
    name: "Sausage",
    price: 3,
  },
]);

const totalPrice = computed(() => {
  let totalPrice = 0;
  cardItems.value.forEach(({ total }) => {
    totalPrice += total;
  });
  return totalPrice;
});
watch(modal, (value) => {
  if (value === false) {
    selectedToppings.value = [];
    selectedItem.value = null;
  }
});
</script>

<template>
  <div>
    <nav
      class="
        flex
        items-center
        justify-between
        max-w-screen
        p-4
        mx-auto
        border-b-2
        bg-secondary
        text-white
      "
    >
      <a
        class="
          inline-flex
          items-center
          justify-center
          w-10
          h-10
          bg-gray-100
          rounded-lg
        "
        href="/"
      >
        Pizza
      </a>

      <ul class="flex items-center space-x-2 text-sm font-medium text-gray-500">
        <li class="hidden lg:block">
          <a class="px-3 py-2 rounded-lg" href="/"> Home </a>
        </li>

        <li>
          <a
            class="px-3 py-2 rounded-lg"
            href="https://github.com/silvesterwali/pre_test_front_end"
          >
            Silvester Wali
          </a>
        </li>
      </ul>
    </nav>
    <section>
      <div class="max-w-screen-xl px-4 py-12 mx-auto sm:px-6 lg:px-8">
        <div class="grid grid-cols-1 gap-4 lg:grid-cols-4 lg:items-start">
          <div class="lg:col-span-3 max-screen">
            <h1 class="font-medium text-4xl">Pizza List</h1>
            <div
              class="grid grid-cols-1 gap-2 mt-4 sm:grid-cols-2 lg:grid-cols-3"
            >
              <div v-for="(item, index) in items" :key="index">
                <Card :item="item" @addItem="addItem"></Card>
              </div>
            </div>
          </div>
          <div class="lg:sticky lg:top-4 bg-white p-3 rounded-lg">
            <h1 class="font-lg text-2xl">Cart</h1>
            <div
              class="h-36 text-center flex items-center"
              v-if="!cardItems.length"
            >
              <span class="items-center">
                The Shopping cart is still empty,click item to add to card
              </span>
            </div>
            <div v-else class="mb-5">
              <div v-for="(item, index) in cardItems" :key="index">
                <ItemCartVue
                  :itemCart="item"
                  @removeItem="removeItem"
                  :index="index"
                ></ItemCartVue>
              </div>
            </div>

            <div
              class="flex justify-between bg-black text-white rounded-lg p-2"
            >
              <span>Total</span> <span>${{ totalPrice }}</span>
            </div>
          </div>
        </div>
      </div>
    </section>
    <Modal v-model="modal" title="Toppings" @addItemToCart="addItemToCart">
      <div class="grid grid-cols-3 gap-4">
        <div v-for="(topping, index) in toppings" :key="index">
          <label>
            <input
              v-model="selectedToppings"
              :value="topping"
              type="checkbox"
              class="mr-2 ml-1"
            />{{ topping.name }}(${{ topping.price }})
          </label>
        </div>
      </div>
    </Modal>
  </div>
</template>

<style>
</style>

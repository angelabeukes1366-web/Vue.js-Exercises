<template>
  <div class="container mt-4">
    <h1 class="mb-4">Cooking Masterclass Checkout</h1>

    <div class="row">
      <div class="col-md-8">
        <div class="row">
          <div v-for="course in courses" :key="course.id" class="col-md-6 mb-3">
            <CourseCard :course="course" @add-to-cart="addToCart" />
          </div>
        </div>
      </div>

      <div class="col-md-4">
        <CartPanel
          :cart="cart"
          :subtotal="subtotal"
          :tax="tax"
          :total="total"
          @increase="increaseQty"
          @decrease="decreaseQty"
          @remove-item="removeItem"
          @clear-cart="clearCart"
        />
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, watch } from "vue";
import CourseCard from "./components/CourseCard.vue";
import CartPanel from "./components/CartPanel.vue";

const courses = ref([
  {
    id: 1,
    title: "Italian Pasta Masterclass",
    description: "Learn authentic pasta making.",
    price: 450,
    stock: 5,
  },
  {
    id: 2,
    title: "French Pastry Basics",
    description: "Bake croissants and pastries.",
    price: 550,
    stock: 3,
  },
  {
    id: 3,
    title: "Sushi Fundamentals",
    description: "Prepare sushi like a pro.",
    price: 650,
    stock: 2,
  },
  {
    id: 4,
    title: "BBQ Secrets",
    description: "Master grilling techniques.",
    price: 400,
    stock: 0,
  },
]);

const cart = ref(JSON.parse(localStorage.getItem("cart")) || []);

function addToCart(course) {
  const existing = cart.value.find((item) => item.id === course.id);

  if (existing) {
    existing.quantity++;
  } else {
    cart.value.push({
      ...course,
      quantity: 1,
    });
  }
}

function increaseQty(id) {
  const item = cart.value.find((item) => item.id === id);

  item.quantity++;
}

function decreaseQty(id) {
  const item = cart.value.find((item) => item.id === id);

  if (item.quantity > 1) {
    item.quantity--;
  }
}

function removeItem(id) {
  cart.value = cart.value.filter((item) => item.id !== id);
}

function clearCart() {
  cart.value = [];
}

const subtotal = computed(() => {
  return cart.value.reduce((sum, item) => sum + item.price * item.quantity, 0);
});

const tax = computed(() => subtotal.value * 0.15);

const total = computed(() => {
  return subtotal.value + tax.value;
});

watch(
  cart,
  () => {
    localStorage.setItem("cart", JSON.stringify(cart.value));
  },
  { deep: true },
);
</script>

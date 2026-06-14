<template>
  <div>
    <h3>Shopping Cart</h3>

    <div v-if="cart.length === 0">Cart is empty.</div>

    <div v-for="item in cart" :key="item.id" class="border p-2 mb-2">
      <h6>{{ item.title }}</h6>

      <p>R{{ item.price }}</p>

      <div class="d-flex gap-2 align-items-center">
        <button
          class="btn btn-sm btn-secondary"
          @click="$emit('decrease', item.id)"
        >
          -
        </button>

        <span>{{ item.quantity }}</span>

        <button
          class="btn btn-sm btn-secondary"
          @click="$emit('increase', item.id)"
        >
          +
        </button>
      </div>

      <p class="mt-2">
        Line Total:
        <strong> R{{ item.price * item.quantity }} </strong>
      </p>

      <button
        class="btn btn-danger btn-sm"
        @click="$emit('remove-item', item.id)"
      >
        Remove
      </button>
    </div>

    <hr />

    <p>Subtotal: R{{ subtotal.toFixed(2) }}</p>
    <p>Tax (15%): R{{ tax.toFixed(2) }}</p>

    <h4>Grand Total: R{{ total.toFixed(2) }}</h4>

    <button class="btn btn-warning" @click="$emit('clear-cart')">
      Clear Cart
    </button>
  </div>
</template>

<script setup>
defineProps({
  cart: Array,
  subtotal: Number,
  tax: Number,
  total: Number,
});
</script>

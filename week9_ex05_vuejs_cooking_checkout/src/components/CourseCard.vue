<template>
  <div class="card h-100">
    <div class="card-body">
      <h5>{{ course.title }}</h5>

      <p>{{ course.description }}</p>

      <p>
        <strong>R{{ course.price }}</strong>
      </p>

      <span v-if="course.stock === 0" class="badge bg-danger"> Sold Out </span>

      <button
        v-else
        class="btn btn-primary"
        @click="$emit('add-to-cart', course)"
      >
        Add To Cart
      </button>
    </div>
  </div>
</template>

<script setup>
defineProps({
  course: Object,
});
</script>

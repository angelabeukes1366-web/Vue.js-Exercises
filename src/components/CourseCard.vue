<template>
  <div class="card">
    <h3>{{ course.title }}</h3>

    <p><strong>Chef:</strong> {{ course.chef }}</p>

    <p><strong>Level:</strong> {{ course.level }}</p>

    <p><strong>Price:</strong> R{{ course.price }}</p>

    <p v-if="!course.available" class="soldout">SOLD OUT</p>

    <button @click="$emit('save-course')" :disabled="!course.available">
      Save to Wishlist
    </button>
  </div>
</template>

<script>
export default {
  props: {
    course: Object,
  },
};
</script>

<style scoped>
.card {
  background: white;
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0 2px 6px rgba(0, 0, 0, 0.2);
}

button {
  width: 100%;
  padding: 10px;
  border: none;
  background: #d35400;
  color: white;
  border-radius: 5px;
  cursor: pointer;
}

button:disabled {
  background: gray;
  cursor: not-allowed;
}

.soldout {
  color: red;
  font-weight: bold;
}
</style>
s

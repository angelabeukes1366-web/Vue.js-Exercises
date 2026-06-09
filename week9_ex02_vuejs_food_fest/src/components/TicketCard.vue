<template>
  <div class="card" :class="{ featured: ticket.featured }">
    <div v-if="ticket.featured" class="badge">Featured</div>

    <h2>{{ ticket.name }}</h2>

    <h3>R{{ ticket.price }}</h3>

    <ul>
      <li v-for="benefit in ticket.benefits" :key="benefit">
        {{ benefit }}
      </li>
    </ul>

    <button class="fav-btn" @click="$emit('toggle-favourite', ticket.id)">
      {{ ticket.favourite ? "❤️ Favourited" : "🤍 Favourite" }}
    </button>
  </div>
</template>

<script setup>
defineProps({
  ticket: Object,
});

defineEmits(["toggle-favourite"]);
</script>
s

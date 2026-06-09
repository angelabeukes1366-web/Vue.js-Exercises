<template>
  <div class="app">
    <header class="hero">
      <h1>Cape Town Food Fest 2026</h1>
      <p>
        Join South Africa's biggest food celebration featuring chefs, street
        food vendors, live music and family entertainment.
      </p>
    </header>

    <section class="tickets">
      <TicketCard
        v-for="ticket in sortedTickets"
        :key="ticket.id"
        :ticket="ticket"
        @toggle-favourite="toggleFavourite"
      />
    </section>

    <footer>
      <p>Food Fest Landing Page - Vue 3</p>
    </footer>
  </div>
</template>

<script setup>
import { ref, computed } from "vue";
import TicketCard from "./components/TicketCard.vue";

const tickets = ref([
  {
    id: 1,
    name: "Bronze",
    price: 150,
    featured: false,
    favourite: false,
    benefits: ["Festival Entry", "Food Market Access", "Live Music Area"],
  },
  {
    id: 2,
    name: "Silver",
    price: 300,
    featured: true,
    favourite: false,
    benefits: [
      "Festival Entry",
      "VIP Seating",
      "Exclusive Tastings",
      "Live Entertainment",
    ],
  },
  {
    id: 3,
    name: "Gold",
    price: 500,
    featured: false,
    favourite: false,
    benefits: [
      "All Silver Benefits",
      "Chef Meet & Greet",
      "Fast Track Entry",
      "Premium Lounge Access",
    ],
  },
]);

const sortedTickets = computed(() => {
  return [...tickets.value].sort((a, b) => a.price - b.price);
});

const toggleFavourite = (id) => {
  const ticket = tickets.value.find((t) => t.id === id);

  if (ticket) {
    ticket.favourite = !ticket.favourite;
  }
};
</script>

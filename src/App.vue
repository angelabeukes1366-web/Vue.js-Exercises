<template>
  <div class="container">
    <header>
      <h1>🍳 Cooking Masterclass Catalogue</h1>
      <h2>❤️ Wishlist: {{ wishlistCount }}</h2>
    </header>

    <div class="courses">
      <CourseCard
        v-for="course in courses"
        :key="course.id"
        :course="course"
        @save-course="addToWishlist"
      />
    </div>
  </div>
</template>

<script>
import CourseCard from "./components/CourseCard.vue";

export default {
  components: {
    CourseCard,
  },
  data() {
    return {
      wishlistCount: 0,
      courses: [
        {
          id: 1,
          title: "Italian Pasta Mastery",
          chef: "Chef Marco Rossi",
          level: "Beginner",
          price: 499,
          available: true,
        },
        {
          id: 2,
          title: "Sushi Fundamentals",
          chef: "Chef Aiko Tanaka",
          level: "Intermediate",
          price: 699,
          available: true,
        },
        {
          id: 3,
          title: "French Pastry Essentials",
          chef: "Chef Pierre Dubois",
          level: "Advanced",
          price: 899,
          available: false,
        },
        {
          id: 4,
          title: "BBQ Secrets",
          chef: "Chef James Smith",
          level: "Beginner",
          price: 399,
          available: true,
        },
      ],
    };
  },
  methods: {
    addToWishlist() {
      this.wishlistCount++;
    },
  },
};
</script>

<style>
body {
  margin: 0;
  font-family: Arial, sans-serif;
  background: #f4f4f4;
}

.container {
  padding: 20px;
}

header {
  text-align: center;
  margin-bottom: 30px;
}

header h1 {
  color: #d35400;
}

.courses {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 20px;
}
</style>

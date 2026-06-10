<template>
  <div class="container">
    <header>
      <h1>🏠 Homes & Beyond</h1>
      <p>Total Properties: {{ filteredProperties.length }}</p>

      <div class="controls">
        <input
          v-model="searchTerm"
          type="text"
          placeholder="Search by title or location..."
        />

        <select v-model="sortOrder">
          <option value="low">Price: Low to High</option>
          <option value="high">Price: High to Low</option>
        </select>
      </div>
    </header>

    <div class="property-grid">
      <div
        v-for="property in filteredProperties"
        :key="property.id"
        class="property-card"
      >
        <div class="image-wrapper">
          <img :src="property.image" :alt="property.title" />

          <span v-if="!property.available" class="badge unavailable">
            Not Available
          </span>

          <button class="favorite-btn" @click="toggleFavorite(property)">
            {{ property.favorite ? "❤️" : "🤍" }}
          </button>
        </div>

        <div class="card-content">
          <h2>{{ property.title }}</h2>
          <p>📍 {{ property.location }}</p>
          <p>🏡 {{ property.type }}</p>
          <p class="price">R{{ property.price.toLocaleString() }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      searchTerm: "",
      sortOrder: "low",

      properties: [
        {
          id: 1,
          title: "Luxury Sea View Apartment",
          location: "Cape Town",
          price: 2500,
          type: "Apartment",
          available: true,
          favorite: false,
          image: "https://images.unsplash.com/photo-1502672260266-1c1ef2d93688",
        },
        {
          id: 2,
          title: "Modern Family House",
          location: "Durbanville",
          price: 4200,
          type: "House",
          available: true,
          favorite: false,
          image: "https://images.unsplash.com/photo-1568605114967-8130f3a36994",
        },
        {
          id: 3,
          title: "Beachfront Villa",
          location: "Camps Bay",
          price: 6500,
          type: "Villa",
          available: false,
          favorite: false,
          image: "https://images.unsplash.com/photo-1512917774080-9991f1c4c750",
        },
        {
          id: 4,
          title: "City Studio",
          location: "Cape Town CBD",
          price: 1800,
          type: "Studio",
          available: true,
          favorite: false,
          image: "https://images.unsplash.com/photo-1494526585095-c41746248156",
        },
        {
          id: 5,
          title: "Garden Cottage",
          location: "Constantia",
          price: 3200,
          type: "Cottage",
          available: false,
          favorite: false,
          image: "https://images.unsplash.com/photo-1570129477492-45c003edd2be",
        },
      ],
    };
  },

  computed: {
    filteredProperties() {
      let result = this.properties.filter(
        (property) =>
          property.title
            .toLowerCase()
            .includes(this.searchTerm.toLowerCase()) ||
          property.location
            .toLowerCase()
            .includes(this.searchTerm.toLowerCase()),
      );

      if (this.sortOrder === "low") {
        result.sort((a, b) => a.price - b.price);
      } else {
        result.sort((a, b) => b.price - a.price);
      }

      return result;
    },
  },

  methods: {
    toggleFavorite(property) {
      property.favorite = !property.favorite;
    },
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  background: #f4f4f4;
  font-family: Arial, sans-serif;
}

.container {
  max-width: 1200px;
  margin: auto;
  padding: 20px;
}

header {
  text-align: center;
  margin-bottom: 30px;
}

header h1 {
  margin-bottom: 10px;
}

.controls {
  margin-top: 20px;
  display: flex;
  gap: 10px;
  justify-content: center;
}

input,
select {
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
}

.property-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 20px;
}

.property-card {
  background: white;
  border-radius: 12px;
  overflow: hidden;
  box-shadow: 0 3px 10px rgba(0, 0, 0, 0.1);
}

.property-card img {
  width: 100%;
  height: 220px;
  object-fit: cover;
}

.image-wrapper {
  position: relative;
}

.badge {
  position: absolute;
  top: 10px;
  left: 10px;
  background: crimson;
  color: white;
  padding: 5px 10px;
  border-radius: 5px;
}

.favorite-btn {
  position: absolute;
  top: 10px;
  right: 10px;
  border: none;
  background: white;
  padding: 8px;
  border-radius: 50%;
  cursor: pointer;
}

.card-content {
  padding: 15px;
}

.price {
  margin-top: 10px;
  font-weight: bold;
  color: green;
}
</style>

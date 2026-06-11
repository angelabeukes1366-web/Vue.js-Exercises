<template>
  <div class="container">
    <h1>FlexZone Fitness Scheduler</h1>

    <div class="card">
      <h2>Add New Class</h2>

      <form @submit.prevent="addSession">
        <input v-model="newSession.name" type="text" placeholder="Class Name" />

        <input
          v-model="newSession.coach"
          type="text"
          placeholder="Coach Name"
        />

        <input v-model="newSession.date" type="date" />

        <input v-model="newSession.time" type="time" />

        <input
          v-model.number="newSession.capacity"
          type="number"
          placeholder="Capacity"
          min="1"
        />

        <button type="submit">Add Session</button>
      </form>

      <p class="error" v-if="errorMessage">
        {{ errorMessage }}
      </p>
    </div>

    <div class="card">
      <h2>Scheduled Classes ({{ totalSessions }})</h2>

      <div v-if="sessions.length === 0">
        <p>No sessions scheduled.</p>
      </div>

      <div v-else>
        <div class="session" v-for="(session, index) in sessions" :key="index">
          <h3>{{ session.name }}</h3>
          <p><strong>Coach:</strong> {{ session.coach }}</p>
          <p><strong>Date:</strong> {{ session.date }}</p>
          <p><strong>Time:</strong> {{ session.time }}</p>
          <p><strong>Capacity:</strong> {{ session.capacity }}</p>

          <button class="delete-btn" @click="deleteSession(index)">
            Delete
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from "vue";

const sessions = ref([]);

const newSession = ref({
  name: "",
  coach: "",
  date: "",
  time: "",
  capacity: "",
});

const errorMessage = ref("");

const addSession = () => {
  if (
    !newSession.value.name ||
    !newSession.value.coach ||
    !newSession.value.date ||
    !newSession.value.time ||
    !newSession.value.capacity
  ) {
    errorMessage.value = "Please complete all fields.";
    return;
  }

  sessions.value.push({
    ...newSession.value,
  });

  errorMessage.value = "";

  newSession.value = {
    name: "",
    coach: "",
    date: "",
    time: "",
    capacity: "",
  };
};

const deleteSession = (index) => {
  sessions.value.splice(index, 1);
};

const totalSessions = computed(() => sessions.value.length);
</script>

<style>
* {
  box-sizing: border-box;
}

body {
  margin: 0;
  background: #f4f4f4;
  font-family: Arial, sans-serif;
}

.container {
  max-width: 900px;
  margin: auto;
  padding: 20px;
}

h1 {
  text-align: center;
}

.card {
  background: white;
  padding: 20px;
  margin-bottom: 20px;
  border-radius: 10px;
}

form {
  display: grid;
  gap: 10px;
}

input {
  padding: 10px;
}

button {
  padding: 10px;
  cursor: pointer;
}

.session {
  border: 1px solid #ddd;
  padding: 15px;
  margin-bottom: 10px;
  border-radius: 8px;
}

.delete-btn {
  background: crimson;
  color: white;
  border: none;
}

.error {
  color: red;
  margin-top: 10px;
}

@media (max-width: 600px) {
  .container {
    padding: 10px;
  }
}
</style>

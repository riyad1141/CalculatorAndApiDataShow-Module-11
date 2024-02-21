<script setup>
import { onMounted, ref } from "vue";

let isLoading = ref(true);
let quoteData = ref({});

async function fetchAndAssignQuoteData() {
  try {
    const response = await fetch('https://animechan.xyz/api/random');
    if (!response.ok) {
      throw new Error('Network response was not ok');
    }
    quoteData.value = await response.json();

  } catch (error) {
    console.error('Error fetching data:', error);
  } finally {
    isLoading.value = false;
  }
}

onMounted(fetchAndAssignQuoteData);

</script>

<template>

  <div class="container">
    <div class="card" v-if="!isLoading">
      <div class="card-header">
        API Data
      </div>
      <div class="card-body">
        <div class="form-group">
          <label for="id">ID:</label>
          <input type="text" class="form-control" id="id" :value="quoteData.id" readonly>
        </div>
        <div class="form-group">
          <label for="quote">Quote:</label>
          <input type="text" class="form-control" id="quote" :value="quoteData.quote" readonly>
        </div>
        <div class="form-group">
          <label for="anime">Anime:</label>
          <input type="text" class="form-control" id="anime" :value="quoteData.anime" readonly>
        </div>
        <div class="form-group">
          <label for="character">Character:</label>
          <input type="text" class="form-control" id="character" :value="quoteData.character" readonly>
        </div>
      </div>
    </div>

    <div class="skeleton" v-else>
      <div class="skeleton-header"></div>
      <div class="skeleton-body"></div>
      <div class="skeleton-body"></div>
      <div class="skeleton-body"></div>
      <div class="skeleton-body"></div>
    </div>

  </div>

</template>

<style scoped>

body {
  background-color: #f8f9fa;
}

.container {
  max-width: 600px;
  margin-top: 50px;
}

.card {
  border: none;
  border-radius: 10px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

.card-header {
  background-color: #007bff;
  color: #fff;
  border-radius: 8px 8px 0 0;
}

.form-group {
  margin-bottom: 20px;
}

.skeleton {
  background-color: #ddd;
  border-radius: 10px;
  overflow: hidden;
  animation: skeleton-loading 1s infinite alternate;
}

.skeleton-header {
  height: 40px;
}

.skeleton-body {
  height: 20px;
  margin-bottom: 8px;
}

@keyframes skeleton-loading {
  0% {
    opacity: 0.7;
  }
  100% {
    opacity: 1;
  }
}

</style>

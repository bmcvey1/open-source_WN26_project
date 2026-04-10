<script setup lang="ts">
import { ref } from 'vue'
import type { Restaurant } from './types/restaurants'

import CarouselRow from './components/base/CarouselRow.vue'
import RestaurantModal from './components/base/RestaurantModal.vue'
import { useRestaurants } from './composables/useRestaurants'

const { restaurants, loading } = useRestaurants()

// --- modal state ---
const selectedRestaurant = ref<Restaurant | null>(null)

// --- handlers ---
function openModal(r: Restaurant) {
  selectedRestaurant.value = r
}

function closeModal() {
  selectedRestaurant.value = null
}
</script>

<template>
  <main class="container">
    <div v-if="loading">Loading...</div>

    <template v-else>
      <CarouselRow
        title="Top suggestions based on your preferences"
        :items="restaurants"
        @select="openModal"
      />

      <CarouselRow
        title="TEST"
        :items="restaurants"
        @select="openModal"
      />
    </template>

    <!-- Modal (popout detail view) -->
    <RestaurantModal
      :restaurant="selectedRestaurant"
      @close="closeModal"
    />
  </main>
</template>

<style>
.container {
  padding: 24px;
  max-width: 1200px;
  margin: 0 auto;
}
</style>
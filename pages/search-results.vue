<template>
  <UContainer>
    <div v-if="mediaList.length > 0">
      <h2>Resultados de la búsqueda: "{{ searchQuery }}"</h2>
      
      <ul class="media-list">
        <li v-for="media in mediaList" :key="media.hash" class="media-item">
          <div class="media-info">
            <h3>{{ media.title }}</h3>
            <p>Por: {{ media.creator }}</p>
          </div>
          <UButton @click="goToStream(media.hash)" color="primary">Reproducir</UButton>
        </li>
      </ul>
    </div>
    <div v-else>
      <p>No se encontraron resultados para "{{ searchQuery }}".</p>
    </div>
  </UContainer>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { useRoute, useRouter } from 'vue-router'

const route = useRoute()
const router = useRouter()

const mediaList = ref([])
const searchQuery = ref(route.query.q || '')

const fetchResults = async (query) => {
  try {
    const response = await fetch(`/api/songs?q=${query}`)
    const data = await response.json()

    if (data.count > 0) {
      mediaList.value = data.media
    } else {
      mediaList.value = []
    }
  } catch (error) {
    console.error('Error en la búsqueda:', error)
  }
}

onMounted(() => {
  if (searchQuery.value) {
    fetchResults(searchQuery.value)
  }
})

const goToStream = (hash) => {
  router.push(`/streaming/${hash}`)
}
</script>

<style scoped>
.media-list {
  list-style: none;
  padding: 0;
}

.media-item {
  display: flex;
  justify-content: space-between;
  margin-bottom: 1.5rem;
  padding: 1rem;
  border: 1px solid #ccc;
  border-radius: 8px;
}

.media-info {
  flex: 1;
}

h3 {
  margin: 0;
}

p {
  margin: 0.5rem 0 0;
}
</style>

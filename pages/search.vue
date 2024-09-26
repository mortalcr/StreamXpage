<template>
  <UContainer class="aUContainer">
    <!-- Barra de búsqueda -->
    <UInput 
      v-model="searchTerm" 
      placeholder="Buscar archivos..."
      clearable
      size="lg"
      class="aUInput"
      color="orange"
      fontcolor
    />
    <UButton 
      @click="searchFiles" 
      size="lg"
      class="mb-4" 
      color="orange"
      block
    >
      Buscar
    </UButton>

    <!-- Resultados de la búsqueda -->
    <div v-if="media.length > 0">
      <!-- Mostrar Title y Creator de cada archivo -->
      <div v-for="item in media" :key="item.Hash" class="mb-2">
        <UCard class="aUCard">
          <h3>{{ item.Title }} - {{ item.Creator }}</h3> <!-- Ajustado a la estructura de la API -->
          <UButton color="gray" @click="playMedia(item.Hash)">Reproducir</UButton>
        </UCard>
      </div>
    </div>

    <!-- Mensaje cuando no hay resultados -->
    <div v-else>
      <p>No se encontraron resultados</p>
    </div>
  </UContainer>
</template>

<script setup>
import { ref, onMounted, watch } from 'vue'
import { useRouter, useRoute } from 'vue-router'
import axios from 'axios'

const searchTerm = ref('')
const media = ref([])
const route = useRoute()
const router = useRouter()

// Función para buscar archivos HLS
const searchFiles = async () => {
  try {
    const response = await axios.get(`http://localhost:8080/api/songs?q=${encodeURIComponent(searchTerm.value)}`)
    media.value = response.data.media // Ajustado a la estructura de la API
  } catch (error) {
    console.error("Error al buscar archivos:", error)
  }
}

// Función para reproducir un archivo
const playMedia = (hash) => {
  router.push(`/streaming/${hash}`)
}

// Ejecutar búsqueda automáticamente si hay un término en la query
onMounted(() => {
  if (route.query.q) {
    searchTerm.value = route.query.q
    searchFiles()
  }
})

// Verificar cambios en la query y ejecutar la búsqueda
watch(() => route.query.q, (newQuery) => {
  if (newQuery) {
    searchTerm.value = newQuery
    searchFiles()
  }
})
</script>

<style scoped>
.mb-4 {
  margin-bottom: 1rem;
}
.mb-2 {
  margin-bottom: 0.5rem;
}

.aUCard {
  background-color: #fb923c;
}

.aUContainer {
  color: #ffffff;
}
.aUInput {
  background-color: #ffffff;
  margin-bottom: 4px;
}
</style>

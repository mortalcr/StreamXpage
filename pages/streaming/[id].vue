<template>
  <UContainer>
    <div v-if="media">
      <h2>{{ media.title }}</h2>
      <h4>{{ media.creator }}</h4>

      <div class="flex justify-center">
        <div class="w-4/5 max-w-lg">
          <hls-player :streamUrl="hlsUrl" />
        </div>
      </div>
    </div>
    <div v-else>
      <p>Cargando...</p>
    </div>

    <div class="flex justify-between mt-6">
      <UButton @click="goHome">Ir al inicio</UButton>
    </div>
  </UContainer>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { useRouter, useRoute } from 'vue-router'
import HlsPlayer from '@/components/HLSPlayer.vue'

const route = useRoute()
const router = useRouter()

const media = ref(null)
const hlsUrl = ref('')

// Esta función carga el video utilizando la API
const loadMedia = async (id) => {
  try {
    const response = await fetch(`/api/songs?q=${id}`)
    const data = await response.json()

    if (data.count > 0) {
      media.value = data.media[0]  // Tomamos el primer resultado
      hlsUrl.value = `http://localhost:8080/${media.value.hash}/outputlist.m3u8`
    }
  } catch (error) {
    console.error('Error al cargar el video:', error)
  }
}

// Llama a la API cuando se carga la página
onMounted(() => {
  loadMedia(route.params.id)
})

const goHome = () => {
  router.push('/')
}
</script>

<style scoped>
.flex {
  display: flex;
}
.justify-center {
  justify-content: center;
}
.justify-between {
  justify-content: space-between;
}
.mb-4 {
  margin-bottom: 1rem;
}
.mt-6 {
  margin-top: 1.5rem;
}
.max-w-lg {
  max-width: 800px;
}
</style>

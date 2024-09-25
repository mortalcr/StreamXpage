<template>
  <UContainer>
    <!-- Barra de búsqueda -->
    <UInput 
      v-model="searchUrl" 
      placeholder="Ingresa la URL del stream HLS"
      clearable
      size="lg"
      class="mb-4"
    />
    <Ubutton 
      @click="changeStream" 
      size="lg"
      class="mb-4" 
      block
    >
      Cargar Stream
    </Ubutton>

    <!-- Reproductor centrado -->
    <div class="flex justify-center">
      <div class="w-4/5 max-w-lg">
        <hls-player :streamUrl="hlsUrl" />
      </div>
    </div>

    <!-- Botones de navegación -->
    <div class="flex justify-between mt-6">
      <UButton @click="goHome">Ir al inicio</UButton>
      <UButton @click="uploadVideo" color="primary">Subir video</UButton>
    </div>
  </UContainer>
</template>

<script setup>
import { ref } from 'vue'
import { useRouter } from 'vue-router'
import HlsPlayer from '@/components/HLSPlayer.vue'

const hlsUrl = ref('http://localhost:8080/418193a6-2fb8-5179-9a47-5908365f70b5/outputlist.m3u8')
const searchUrl = ref('')

const changeStream = () => {
  if (searchUrl.value) {
    hlsUrl.value = searchUrl.value
  }
}

const router = useRouter()

const goHome = () => {
  router.push('/')
}

const uploadVideo = () => {
  router.push('/upload-video')
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

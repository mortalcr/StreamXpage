<template>
  <UContainer>
    <UInput 
      v-model="searchUrl" 
      placeholder="Ingresa el nombre del video"
      clearable
      size="lg"
      class="mb-4"
    />
    <UButton 
      @click="searchMedia" 
      size="lg"
      class="mb-4" 
      block
    >
      Buscar
    </UButton>

    <div class="flex justify-center">
      <div class="w-4/5 max-w-lg">
        <hls-player :streamUrl="hlsUrl" />
      </div>
    </div>

    <div class="flex justify-between mt-6">
      <UButton @click="goHome">Ir al inicio</UButton>
      <UButton @click="uploadVideo" color="primary">Subir video</UButton>
    </div>
  </UContainer>
</template>

<script setup>
import { ref } from 'vue'
import { useRouter } from 'vue-router'

const searchUrl = ref('')
const router = useRouter()

const searchMedia = () => {
  if (searchUrl.value) {
    router.push({ path: '/search-results', query: { q: searchUrl.value } })
  }
}

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

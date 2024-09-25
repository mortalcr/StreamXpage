<template>
  <UContainer>
    <div class="search-container mb-4">
      <UInput 
        v-model="searchUrl" 
        placeholder="Buscar archivos HLS..." 
        clearable
        size="lg"
        class="search-bar"
      />
      <UButton 
        @click="redirectToSearch" 
        size="lg"
        color="primary"
        class="search-button"
      > 
      <UIcon name="il:search"></UIcon>
      </UButton>
    </div>

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
import { ref, onMounted } from 'vue'
import { useRoute, useRouter } from 'vue-router'
import HlsPlayer from '@/components/HLSPlayer.vue'

const hlsUrl = ref('')
const searchUrl = ref('')
const route = useRoute()
const router = useRouter()

const redirectToSearch = () => {
  if (searchUrl.value) {
    router.push({ path: '/search', query: { q: searchUrl.value } })
  }
}

const goHome = () => {
  router.push('/')
}

const uploadVideo = () => {
  router.push('/upload-video')
}

onMounted(() => {
  const hash = route.params.id
  hlsUrl.value = `http://localhost:8080/${hash}/outputlist.m3u8`
})
</script>

<style scoped>

.search-container {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.search-bar {
  flex: 1;
}

.search-button {
  margin-left: 10px;
  display: flex;
  align-items: center;
  justify-content: center;
}

@import url('https://cdn.materialdesignicons.com/5.4.55/css/materialdesignicons.min.css');

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

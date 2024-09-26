<template>
  <UContainer>
    <div class="search-container mb-4">
      <UInput 
        v-model="searchUrl" 
        placeholder="Buscar archivos HLS..." 
        clearable
        size="lg"
        class="search-bar"
        color="orange"
      />
      <UButton 
        @click="redirectToSearch" 
        size="lg"
        color="orange"
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

onMounted(() => {
  const hash = route.params.id
  hlsUrl.value = `http://localhost:8080/${hash}/${hash}.m3u8`
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
  background-color: #ffffff90;
  margin-bottom: 4px;
}

.search-button {
  margin-left: 10px;
  display: flex;
  align-items: center;
  justify-content: center;
}

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

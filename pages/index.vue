<template>
  <div class="index-container">
    <UCard class="u-card">
      <h1>Bienvenido a nuestro reproductor de video HLS</h1>
      <p>Explora, sube y reproduce videos en formato HLS de manera fácil y rápida.</p>
      <UButton color="orange" @click="goToSearch">Explorar</UButton>
    </UCard>
  </div>
</template>

<script setup>
import { useRouter } from 'vue-router'
const router = useRouter()

const goToSearch = () => {
  router.push('/search')
}
</script>

<style scoped>
.index-container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 90vh;
  background-color: #1e1b29; /* Fondo oscuro */
}

.u-card {
  padding: 20px;
  background-color: #1e1b29; /* Fondo oscuro */
  color: #ffffff;
  text-align: center;
}

u-button {
  background-color: #f97316; /* Naranja vivo */
  color: #ffffff;
}
</style>

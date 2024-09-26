<template>
  <div class="h-[100vh] w-full bg-slate-800">
    <!-- Navbar -->
    <nav class="navbar">
      <ul class="navbar-menu">
        <li>
          <NuxtLink to="/">
            <UButton color="primary" size="lg" class="navbar-button">Inicio</UButton>
          </NuxtLink>
        </li>
        <li>
          <NuxtLink to="/upload-video">
            <UButton color="secondary" size="lg" class="navbar-button">Subir Video</UButton>
          </NuxtLink>
        </li>
      </ul>
    </nav>

    <!-- Contenido de la página -->
    <NuxtPage/>
  </div>
</template>

<script setup>
</script>

<style scoped>
/* Estilos para la navbar */
.navbar {
  background-color: #1e1b29; /* Fondo oscuro */
  padding: 1rem;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.navbar-menu {
  list-style: none;
  display: flex;
  justify-content: flex-start;
  gap: 20px;
}

.navbar-menu li {
  display: inline-block;
}

.navbar-button {
  text-transform: uppercase;
  font-weight: bold;
  border-radius: 5px;
  background-color: #f97316; /* Naranja vivo */
  color: #ffffff; /* Texto blanco */
  transition: background-color 0.3s ease;
}

.navbar-button:hover {
  background-color: #fb923c; /* Naranja claro para hover */
}
</style>

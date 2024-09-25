<template>
  <div>
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
// No se necesita código adicional para este layout básico
</script>

<style scoped>
/* Estilos para la navbar */
.navbar {
  background-color: #1e3a8a; /* Fondo de la navbar */
  padding: 1rem;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1); /* Sombra sutil */
}

.navbar-menu {
  list-style: none;
  display: flex;
  justify-content: flex-start; /* Alineación de los botones */
  gap: 20px; /* Espacio entre los botones */
}

.navbar-menu li {
  display: inline-block;
}

/* Estilos específicos para los botones dentro de la navbar */
.navbar-button {
  text-transform: uppercase;
  font-weight: bold;
  border-radius: 5px;
  transition: background-color 0.3s ease;
}

.navbar-button:hover {
  background-color: #2563eb; /* Cambio de color en hover */
}
</style>

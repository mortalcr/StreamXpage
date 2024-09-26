<template>
  <div class="h-[85.8vh] w-full bg-slate-800">
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
        <li>
          <NuxtLink to="/search">
            <UButton color="secondary" size="lg" class="navbar-button">Buscar</UButton>
          </NuxtLink>
        </li>
      </ul>
    </nav>
    
    <!-- Contenido de la página -->
    <NuxtPage/>
  </div>
  <footer
            class="w-full min-h-[100px] flex flex-row justify-around bg-slate-600 shadow-[0_1px_3px_2px_rgba(0,0,0,0.2)]">
            <section class="flex flex-col items-start my-5">
                <div>
                    <h1 class="font-bold text-2xl flex-col">Developers</h1>
                </div>
                <div class="w-fit flex flex- gap-4">
                    <Author name="Aaron González" github="https://github.com/zSnails"
                        linked="https://www.linkedin.com/in/aaron-gonz%C3%A1lez-araya-2b48b223a" />
                    <Author name="Daniel Porras" github="https://github.com/mortalcr"
                        linked="https://www.linkedin.com/in/mortalcr" />
                </div>
            </section>
      </footer>
</template>

<script setup>
</script>

<style scoped>
/* Estilos para la navbar */
.navbar {
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

.footer{
  bottom:0px;
}
</style>

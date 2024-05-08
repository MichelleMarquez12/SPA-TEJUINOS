<template>
  <header class="text-white" style="background-color: rgb(94,94,94)">
    <h1 class="text-3xl text-center h-auto text-bold p-1">Directorio de Estudiantes</h1>
  </header>
  <nav class="text-white" style="background-color: rgb(94,94,94)">
    <ul class="flex">
      <li class="p-4">
        <router-link to="/"> Inicio</router-link>
      </li>
      <li class="p-4">
        <router-link to="/estadisticas"> Tablas Estadisticas</router-link>
      </li>
      <li class="p-4">
        <router-link to="/acerca-de"> Acerca de</router-link>
      </li>
    </ul>
  </nav>
  <div>
    <RouterView></RouterView>
  </div>
  
</template>

<script>

</script>
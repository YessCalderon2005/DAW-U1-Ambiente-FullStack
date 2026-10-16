<script setup>
import { useRouter, useRoute } from 'vue-router'

const router = useRouter()
const route = useRoute()

const handleLogout = () => {
  // Limpiamos todo el almacenamiento local por si acaso
  localStorage.clear()
  sessionStorage.clear()
  router.push('/login')
}
</script>

<template>
  <header class="app-header">
    <div class="logo">
      <h1>Aplicación Full Stack</h1>
    </div>
    <nav class="nav-links">
      <router-link to="/dashboard">Inicio</router-link>
      <router-link to="/servicios">Servicios</router-link>
      
      <!-- Si la ruta no es login, mostramos el botón de cerrar sesión directamente -->
      <button v-if="route.path !== '/login'" @click="handleLogout" class="btn-logout">
        Cerrar Sesión
      </button>
      <router-link v-else to="/login" class="link-login">
        Iniciar Sesión
      </router-link>
    </nav>
  </header>
</template>

<style scoped>
.app-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1rem 2rem;
  background-color: #fce4ec;
  border-bottom: 2px solid #f8bbd0;
}

.logo h1 {
  margin: 0;
  color: #ad1457;
  font-size: 1.3rem;
  font-weight: bold;
}

.nav-links {
  display: flex;
  align-items: center;
  gap: 1.5rem;
}

.nav-links a {
  text-decoration: none;
  color: #880e4f;
  font-weight: 600;
}

.btn-logout {
  background-color: #e91e63;
  color: white;
  border: none;
  padding: 0.5rem 1rem;
  border-radius: 6px;
  cursor: pointer;
  font-weight: 600;
  font-size: 0.9rem;
  transition: background-color 0.2s;
}

.btn-logout:hover {
  background-color: #c2185b;
}

.link-login {
  color: #c2185b;
}
</style>
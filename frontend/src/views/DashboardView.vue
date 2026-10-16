<script setup>
import { useRouter } from 'vue-router'
import { useAuth } from '../services/auth'

const router = useRouter()
const { user, logout } = useAuth()

const handleLogout = () => {
  // Ejecuta la función de cierre de sesión del servicio o limpia el almacenamiento
  if (logout) {
    logout()
  } else {
    localStorage.removeItem('token')
    localStorage.removeItem('user')
    localStorage.clear()
  }
  // Redirige estrictamente a /login tal como pide la Prueba 5
  router.push('/login')
}
</script>

<template>
  <section class="dashboard">
    <div class="dashboard-hero">
      <div>
        <span class="badge">Panel principal</span>
        <h1>Bienvenido, {{ user?.nombre || 'Administrador Demo' }}</h1>
        <p>Desde este espacio puedes consultar los módulos disponibles de la aplicación.</p>
      </div>
      <div class="hero-icon"></div>
    </div>

    <div class="dashboard-grid">
      <article class="dashboard-card card-blue">
        <span class="card-icon"></span>
        <h2>Servicios</h2>
        <p>Consulta los servicios disponibles mediante la API.</p>
        <RouterLink to="/servicios" class="card-link">
          Consultar servicios →
        </RouterLink>
      </article>

      <article class="dashboard-card card-green">
        <span class="card-icon"></span>
        <h2>Usuario</h2>
        <p>{{ user?.usuario || 'admin' }}</p>
        <strong>{{ user?.rol || 'Administrador' }}</strong>
      </article>

      <article class="dashboard-card card-orange">
        <span class="card-icon"></span>
        <h2>Sesión</h2>
        <p>Acceso autenticado mediante el backend PHP.</p>
        <!-- Botón de Cerrar Sesión requerido por la Prueba 5 -->
        <button @click="handleLogout" class="btn-logout-action">
          Cerrar sesión
        </button>
      </article>
    </div>
  </section>
</template>

<style scoped>
.dashboard {
  padding: 2rem;
  max-width: 1200px;
  margin: 0 auto;
}

.dashboard-hero {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background: linear-gradient(135deg, #fce4ec 0%, #f8bbd0 100%);
  padding: 2.5rem;
  border-radius: 12px;
  margin-bottom: 2rem;
  border: 1px solid #f48fb1;
}

.dashboard-hero h1 {
  color: #880e4f;
  margin: 0.5rem 0;
}

.badge {
  background-color: #ad1457;
  color: white;
  padding: 0.3rem 0.8rem;
  border-radius: 20px;
  font-size: 0.85rem;
  font-weight: 600;
}

.dashboard-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 1.5rem;
}

.dashboard-card {
  background: #ffffff;
  border: 1px solid #f8bbd0;
  border-radius: 12px;
  padding: 1.8rem;
  box-shadow: 0 4px 6px rgba(248, 187, 208, 0.2);
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.dashboard-card h2 {
  color: #880e4f;
  margin-top: 0;
}

.card-link {
  color: #e91e63;
  text-decoration: none;
  font-weight: 600;
  margin-top: 1rem;
  display: inline-block;
}

.card-link:hover {
  text-decoration: underline;
}

/* Estilo para el botón de Cerrar sesión de la Prueba 5 */
.btn-logout-action {
  background-color: #e91e63;
  color: white;
  border: none;
  padding: 0.6rem 1.2rem;
  border-radius: 6px;
  cursor: pointer;
  font-weight: 600;
  font-size: 0.95rem;
  margin-top: 1rem;
  transition: background-color 0.2s;
  width: 100%;
}

.btn-logout-action:hover {
  background-color: #c2185b;
}
</style>
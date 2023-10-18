<template>
  <section class="sidebar" :class="{ 'activo': sidebarActivo }">
    <div class="icono-hamburguesa" @click="toggleSidebar">
      <IconHbgMenu />
    </div>
    <div>
      <img
        class="imagen-perfil"
        :class="{ 'show': sidebarActivo }"
        src="@/assets/tomas.webp"
        alt="It should be me!"
      />
      <div v-if="sidebarActivo" class="nombre-usuario">{{ nombreUsuario }}</div>
    </div>
    <div>
      <router-link v-for="opcion in opcionesMenu" :key="opcion.texto" :to="opcion.ruta">
        <div class="opcion-menu">
          <component :is="opcion.icono" #icon></component>
          <span v-if="sidebarActivo">{{ opcion.texto }}</span>
        </div>
      </router-link>
    </div>
  </section>
</template>

<script>
import IconHbgMenu from './icons/IconHbgMenu.vue'
import IconHome from './icons/IconHome.vue'
import IconReport from './icons/IconReport.vue'
import IconFire from './icons/IconFire.vue'

export default {
  props: {
    nombreUsuario: String
  },
  data() {
    return {
      sidebarActivo: false,
      opcionesMenu: [
        { icono: IconHome, texto: 'Home', ruta: { name: 'home' } },
        { icono: IconReport, texto: 'Reportes', ruta: '' }, // Esta ruta está vacía. Puedes ajustarla más adelante.
        { icono: IconFire, texto: 'About', ruta: { name: 'about' } }
      ]
    }
  },
  components: {
    IconHbgMenu,
    IconHome,
    IconReport,
    IconFire
  },
  methods: {
    toggleSidebar() {
      this.sidebarActivo = !this.sidebarActivo
    }
  }
}

</script>
  
<style scoped>
.sidebar {
  width: 50px;
  height: 100vh;
  background-color: #333;
  color: #fff;
  transition: 0.3s ease;
  overflow: hidden;
  display: grid;
  grid-template-rows: auto auto 1fr; /* Ajusta el diseño de las filas */
}

.sidebar.activo {
  width: 250px;
}

.sidebar.activo .icono-hamburguesa {
  justify-content: right;
}

.icono-hamburguesa {
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 20px;
  cursor: pointer;
  padding: 10px;
}

.imagen-perfil {
  width: 40px;
  height: 40px;
  border-radius: 50%;
  margin: 20px auto;
  display: block;
}

.imagen-perfil.show {
  width: 100px;
  height: 100px;
  display: block;
  margin-top: 20px;
}

.nombre-usuario {
  text-align: center;
  font-size: 20px;
  margin-bottom: 20px;
  margin-top: 20px;
}

.opcion-menu {
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 10px;
  cursor: pointer;
  margin-top: 40px; 
}

.sidebar.activo .opcion-menu {
  justify-content: flex-start;
  margin-top: 10px;
}

.sidebar.activo .opcion-menu svg {
  margin-right: 10px;
}
</style>

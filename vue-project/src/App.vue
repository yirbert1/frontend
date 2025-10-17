<template>
  <div id="app">
    <h1>🚀 Clientes App</h1>
    <ClienteList :clientes="clientes" @cliente-registrado="agregarCliente" />
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import axios from 'axios';
import ClienteList from './components/ClienteList.vue';

interface Cliente {
  id_cliente: number;
  nombre: string;
  telefono: string;
  correo: string;
  direccion: string;
}

export default defineComponent({
  components: { ClienteList },
  data() {
    return {
      clientes: [] as Cliente[],
    };
  },
  mounted() {
    this.cargarClientes();
  },
  methods: {
    async cargarClientes() {
      try {
        const res = await axios.get<Cliente[]>('http://localhost:3000/api/cliente');
        this.clientes = res.data;
      } catch (err) {
        console.error('❌ Error cargando clientes:', err);
      }
    },
    agregarCliente(nuevo: Cliente) {
      this.clientes.push(nuevo);
    },
  },
});
</script>

<style scoped>
/* Fondo general con un degradado sutil */
#app {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: flex-start;
  padding: 40px 20px;
  border-radius: 0.9%;
  background: linear-gradient(135deg, #cedfec, #ffffff);
  font-family: 'Segoe UI', Roboto, Helvetica, sans-serif;
  color: #000000;
}

/* Título principal */
h1 {
  font-size: 2rem;
  color: #2c3e50;
  margin-bottom: 30px;
  display: flex;
  align-items: center;
  gap: 10px;
  border-bottom: 5px solid #0099ff;
  padding-bottom: 8px;
}

/* Responsive */
@media (max-width: 600px) {
  h1 {
    font-size: 1.5rem;
    text-align: center;
  }

  #app {
    padding: 20px 10px;
  }
}
</style>


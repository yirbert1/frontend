<template>
  <div class="cliente-container">
    <h2>📝 Registrar Cliente</h2>

    <form @submit.prevent="registrarCliente" class="formulario-cliente">
      <input v-model="clienteNuevo.nombre" placeholder="Nombre" required />
      <input v-model="clienteNuevo.apellido" placeholder="Apellido" required />
      <button type="submit">Registrar</button>
    </form>

    <hr />

    <h2>📋 Lista de Clientes</h2>
    <table class="tabla-clientes">
      <thead>
        <tr>
          <th>ID</th>
          <th>Nombre</th>
          <th>Apellido</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="cliente in clientes" :key="cliente.id">
          <td>{{ cliente.id }}</td>
          <td>{{ cliente.nombre }}</td>
          <td>{{ cliente.apellido }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script lang="ts">
import { defineComponent, type PropType } from 'vue';
import axios from 'axios';

interface Cliente {
  id: number;
  nombre: string;
  apellido: string;
}

export default defineComponent({
  name: 'ClienteList',
  props: {
    clientes: {
      type: Array as PropType<Cliente[]>,
      required: true,
    },
  },
  data() {
    return {
      clienteNuevo: {
        nombre: '',
        apellido: '',
      } as Omit<Cliente, 'id'>,
    };
  },
  methods: {
    async registrarCliente() {
      try {
        const respuesta = await axios.post<Cliente>('http://localhost:3000/api/cliente', this.clienteNuevo);
        this.$emit('cliente-registrado', respuesta.data);

        // Resetear el formulario
        this.clienteNuevo = {
          nombre: '',
          apellido: '',
        };

        alert('✅ Cliente registrado con éxito');
      } catch (error) {
        console.error('❌ Error al registrar cliente:', error);
        alert('❌ Ocurrió un error al registrar el cliente. Intenta nuevamente.');
      }
    },
  },
});
</script>

<style>
.cliente-container {
  max-width: 800px;
  margin: 40px auto;
  padding: 20px;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  background-color: #ffffff;
  box-shadow: 0 4px 12px rgb(0, 0, 0);
  border-radius: 10px;
}

h2 {
  color: #000000;
  margin-bottom: 20px;
  border-bottom: 2px solid #3498db;
  padding-bottom: 5px;
}

.formulario-cliente {
  display: flex;
  flex-direction: column;
  gap: 15px;
  margin-bottom: 30px;
}

.formulario-cliente input {
  padding: 12px 14px;
  border: 1px solid #000000;
  border-radius: 6px;
  font-size: 15px;
  transition: border-color 0.3s;
}

.formulario-cliente input:focus {
  border-color: #3498db;
  outline: none;
}

.formulario-cliente button {
  padding: 12px;
  background-color: #3498db;
  color: white;
  font-weight: bold;
  border: none;
  border-radius: 6px;
  cursor: pointer;
  transition: background-color 0.3s, transform 0.2s;
}

.formulario-cliente button:hover {
  background-color: #2980b9;
  transform: scale(1.02);
}

.tabla-clientes {
  width: 100%;
  border-collapse: collapse;
  font-size: 15px;
}

.tabla-clientes th,
.tabla-clientes td {
  padding: 12px 16px;
  text-align: left;
  border-bottom: 1px solid #000000;
}

.tabla-clientes th {
  background-color: #ffffff;
  color: #000000;
}
.tabla-clientes td {
  color: #000000;
}

.tabla-clientes tbody tr:hover {
  background-color: #0022ff;
}
body {
  background-color: #0a1ed0;
}

/* Responsive (móviles) */
@media (max-width: 600px) {
  .cliente-container {
    padding: 15px;
  }

  .formulario-cliente input,
  .formulario-cliente button {
    font-size: 14px;
  }

  .tabla-clientes th,
  .tabla-clientes td {
    padding: 10px;
    font-size: 14px;
  }
}
</style>

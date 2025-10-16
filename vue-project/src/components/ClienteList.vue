<template>
  <div>
    <h2>📋 Lista de Clientes</h2>
    <table border="1" cellpadding="8">
      <thead>
        <tr>
          <th>ID</th>
          <th>Nombre</th>
          <th>Teléfono</th>
          <th>Correo</th>
          <th>Dirección</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="cliente in clientes" :key="cliente.id_cliente">
          <td>{{ cliente.id_cliente }}</td>
          <td>{{ cliente.nombre }}</td>
          <td>{{ cliente.telefono }}</td>
          <td>{{ cliente.correo }}</td>
          <td>{{ cliente.direccion }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script lang="ts">
import { defineComponent, type PropType } from "vue"; // 👈 nota el "type" aquí

// 💡 Definición del tipo Cliente
interface Cliente {
  id_cliente: number;
  nombre: string;
  telefono: string;
  correo: string;
  direccion: string;
}

export default defineComponent({
  name: "ClienteList",
  props: {
    clientes: {
      type: Array as PropType<Cliente[]>, // 👈 usa el tipo correctamente
      required: true,
    },
  },
});
</script>

<style scoped>
table {
  width: 90%;
  margin: 30px auto;
  border-collapse: separate;
  border-spacing: 0;
  border-radius: 8px;
  overflow: hidden;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
  background-color: #ffffff;
}

th {
  background-color: #4a90e2;
  color: #ffffff;
  text-align: left;
  padding: 12px 16px;
  font-weight: 600;
  font-size: 14px;
  letter-spacing: 0.5px;
}

td {
  padding: 12px 16px;
  border-top: 1px solid #f0f0f0;
  font-size: 14px;
  color: #333333;
}

tr:nth-child(even) {
  background-color: #f9f9f9;
}

tr:hover {
  background-color: #eef6ff;
  transition: background-color 0.2s ease-in-out;
}

h2 {
  text-align: center;
  font-size: 24px;
  margin-top: 40px;
  color: #333;
}
</style>

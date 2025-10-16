
<template>
  <div>
    <h2>Hola desde el componente Hol.vue 🎉</h2>
    
    
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import axios from 'axios'

const usuarios = ref([])

onMounted(async () => {
  try {
    const response = await axios.get('http://localhost:5173/backend') 
    usuarios.value = response.data
  } catch (error) {
    console.error('Error al obtener usuarios:', error)
  }
})
</script>

<style scoped>
h2 {
  color: #42b983;
}

table {
  border-collapse: collapse;
  width: 100%;
  margin-top: 1rem;
}

th, td {
  border: 1px solid #ddd;
  padding: 8px;
}
</style>

<template>
    <div class="user-list">
      <p v-if="loading" class="loading">Memuat data...</p>
      <p v-if="error" class="error">{{ error }}</p>
  
      <ul v-if="!loading && !error" class="user-grid">
        <li v-for="user in users" :key="user.id" class="user-item">
          {{ user.name }}
        </li>
      </ul>
    </div>
  </template>
  
  <script lang="ts" setup>
  import { ref, onMounted } from 'vue';
  import axios from 'axios';
  
  const users = ref([]);
  const loading = ref(true);
  const error = ref('');
  
  onMounted(async () => {
    try {
      const response = await axios.get('https://jsonplaceholder.typicode.com/users');
      users.value = response.data;
    } catch (err) {
      console.error('Error fetching users:', err);
      error.value = 'Gagal mengambil data.';
    } finally {
      loading.value = false;
    }
  });
  </script>
  
  <style scoped>
  .user-list {
    max-width: 800px;
    margin: 20px auto;
    padding: 20px;
    background-color: #f9f9f9;
    border-radius: 8px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  }
  
  .loading {
    color: #4a90e2;
    text-align: center;
    font-size: 1.2rem;
  }
  
  .error {
    color: #d9534f;
    text-align: center;
    font-weight: bold;
  }
  
  .user-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
    gap: 15px;
    list-style-type: none;
    padding: 0;
  }
  
  .user-item {
    background-color: #ffffff;
    padding: 15px;
    border: 1px solid #ddd;
    border-radius: 5px;
    text-align: center;
    transition: transform 0.3s, box-shadow 0.3s;
  }
  
  .user-item:hover {
    transform: scale(1.05);
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
  }
  </style>
  
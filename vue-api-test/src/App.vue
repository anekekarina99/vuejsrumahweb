<template>
  <div class="app-container">
    <h1 class="app-title">Vue 3 Test App</h1>
    <div class="content">
      <UserList />
      <UserForm />
      <PostPagination />
      <LoginForm />
    </div>
  </div>
</template>

<script lang="ts" setup>
import UserList from './components/UserList.vue';
import UserForm from './components/UserForm.vue';
import PostPagination from './components/PostPagination.vue';
import LoginForm from './components/LoginForm.vue';
</script>

<style scoped>
.app-container {
  background-color: #f0f8ff; /* Warna biru muda untuk latar belakang */
  color: #333;
  min-height: 100vh;
  padding: 20px;
  font-family: 'Arial', sans-serif;
}

.app-title {
  font-size: 2.5rem;
  color: #ff6347; /* Warna oranye terang untuk judul */
  text-align: center;
  margin-bottom: 20px;
}

.content {
  display: grid;
  gap: 20px;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  padding: 10px;
}

h1, label, button {
  color: #4a90e2; /* Warna biru terang untuk teks */
}

button {
  background-color: #ff7f50; /* Warna oranye terang untuk tombol */
  color: white;
  border: none;
  padding: 12px 24px;
  border-radius: 5px;
  cursor: pointer;
  font-size: 1rem;
  transition: background-color 0.3s ease;
}

button:hover {
  background-color: #ff4500; /* Hover color */
}

input, textarea {
  border: 2px solid #4a90e2;
  border-radius: 5px;
  padding: 12px;
  width: 100%;
  box-sizing: border-box;
  font-size: 1rem;
}

@media (max-width: 768px) {
  .app-title {
    font-size: 2rem;
  }

  button {
    padding: 10px 20px;
    font-size: 0.9rem;
  }

  input, textarea {
    padding: 10px;
  }
}
</style>

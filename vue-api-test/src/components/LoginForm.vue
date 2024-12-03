<template>
    <div class="login-container">
      <form @submit.prevent="login" class="login-form">
        <label for="username">Username:</label>
        <input id="username" v-model="username" required />
    
        <label for="password">Password:</label>
        <input id="password" v-model="password" type="password" required />
    
        <button type="submit">Login</button>
    
        <p v-if="message" class="message">{{ message }}</p>
      </form>
    </div>
  </template>
    
  <script lang="ts" setup>
  import { ref } from 'vue';
  import axios from 'axios';
  
  const username = ref('');
  const password = ref('');
  const message = ref('');
  
  const login = async () => {
    try {
      const response = await axios.post('https://fictitious-api.com/login', {
        username: username.value,
        password: password.value
      });
  
      localStorage.setItem('token', response.data.token);
      message.value = 'Login Successful';
    } catch (error) {
      console.error('Login failed:', error);
      message.value = 'Login Failed';
    }
  };
  </script>
    
  <style scoped>
  .login-container {
    display: flex;
    justify-content: center;
    align-items: center;
    min-height: 100vh;
    background-color: #f4f4f9;
  }
  
  .login-form {
    display: flex;
    flex-direction: column;
    width: 100%;
    max-width: 400px;
    padding: 20px;
    background-color: #fff;
    border-radius: 8px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  }
  
  label {
    margin-top: 15px;
    font-size: 1.1rem;
  }
  
  input {
    margin-bottom: 15px;
    padding: 12px;
    font-size: 1rem;
    border: 1px solid #ddd;
    border-radius: 5px;
    box-sizing: border-box;
  }
  
  button {
    padding: 12px;
    background-color: #007bff;
    color: white;
    border: none;
    border-radius: 5px;
    font-size: 1rem;
    cursor: pointer;
    transition: background-color 0.3s ease-in-out;
  }
  
  button:hover {
    background-color: #0056b3;
  }
  
  .message {
    margin-top: 15px;
    color: red;
    font-size: 0.9rem;
    text-align: center;
  }
  
  @media (max-width: 600px) {
    .login-form {
      padding: 15px;
    }
  
    input, button {
      font-size: 0.9rem;
    }
  }
  </style>
  
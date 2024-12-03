<template>
    <form @submit.prevent="submitForm" class="contact-form">
      <label for="name">Nama:</label>
      <input id="name" v-model="form.name" required placeholder="Masukkan nama Anda" />
  
      <label for="email">Email:</label>
      <input id="email" v-model="form.email" type="email" required placeholder="Masukkan email Anda" />
  
      <label for="message">Pesan:</label>
      <textarea id="message" v-model="form.message" required placeholder="Masukkan pesan Anda"></textarea>
  
      <button type="submit" :disabled="isSubmitting">Kirim</button>
  
      <p v-if="notification" class="notification">{{ notification }}</p>
    </form>
  </template>
  
  <script lang="ts" setup>
  import { ref } from 'vue';
  import axios from 'axios';
  
  // Form state
  const form = ref({
    name: '',
    email: '',
    message: ''
  });
  
  // Notification message
  const notification = ref('');
  const isSubmitting = ref(false);
  
  // Submit form function
  const submitForm = async () => {
    isSubmitting.value = true;
    try {
      await axios.post('https://jsonplaceholder.typicode.com/posts', form.value);
      notification.value = 'Pengiriman berhasil!';
      form.value = { name: '', email: '', message: '' }; // Reset form after successful submission
    } catch (error) {
      console.error('Error submitting form:', error);
      notification.value = 'Pengiriman gagal!';
    } finally {
      isSubmitting.value = false;
    }
  };
  </script>
  
  <style scoped>
  .contact-form {
    display: flex;
    flex-direction: column;
    max-width: 500px;
    margin: 20px auto;
    background-color: #f9f9f9;
    padding: 20px;
    border-radius: 8px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  }
  
  label {
    margin-top: 10px;
    font-size: 1rem;
    font-weight: 500;
  }
  
  input,
  textarea {
    margin-bottom: 15px;
    padding: 12px;
    width: 100%;
    border: 2px solid #ddd;
    border-radius: 5px;
    font-size: 1rem;
  }
  
  input:focus,
  textarea:focus {
    border-color: #4a90e2; /* Border color when focused */
    outline: none;
  }
  
  button {
    padding: 12px 20px;
    background-color: #007bff;
    color: white;
    border: none;
    border-radius: 5px;
    font-size: 1rem;
    cursor: pointer;
    transition: background-color 0.3s;
  }
  
  button:hover {
    background-color: #0056b3;
  }
  
  button:disabled {
    background-color: #ccc;
    cursor: not-allowed;
  }
  
  .notification {
    margin-top: 15px;
    color: green;
    font-size: 1rem;
    font-weight: bold;
  }
  
  .notification.error {
    color: red;
  }
  
  @media (max-width: 600px) {
    .contact-form {
      padding: 15px;
      max-width: 100%;
    }
  }
  </style>
  
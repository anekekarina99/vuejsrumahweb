<template>
    <div class="pagination-container">
      <h1>Post Pagination</h1>
      <ul class="post-list">
        <li v-for="post in paginatedPosts" :key="post.id">{{ post.title }}</li>
      </ul>
      <div class="pagination-controls">
        <button @click="prevPage" :disabled="page === 1">Previous</button>
        <button @click="nextPage" :disabled="isLastPage">Next</button>
      </div>
    </div>
  </template>
  
  <script lang="ts" setup>
  import { ref, computed, onMounted } from 'vue';
  import axios from 'axios';
  
  // State variables
  const posts = ref([]);
  const page = ref(1);
  const postsPerPage = 5;
  
  // Computed property for paginated posts
  const paginatedPosts = computed(() => {
    const start = (page.value - 1) * postsPerPage;
    return posts.value.slice(start, start + postsPerPage);
  });
  
  // Computed property to disable "Next" button if on the last page
  const isLastPage = computed(() => {
    return page.value * postsPerPage >= posts.value.length;
  });
  
  // Fetch posts on component mount
  const fetchPosts = async () => {
    try {
      const response = await axios.get('https://jsonplaceholder.typicode.com/posts');
      posts.value = response.data;
    } catch (error) {
      console.error('Error fetching posts:', error);
    }
  };
  
  // Pagination controls
  const nextPage = () => {
    if (!isLastPage.value) page.value++;
  };
  const prevPage = () => {
    if (page.value > 1) page.value--;
  };
  
  // Load posts when component is mounted
  onMounted(fetchPosts);
  </script>
  
  <style scoped>
  .pagination-container {
    max-width: 800px;
    margin: 0 auto;
    padding: 20px;
    font-family: 'Arial', sans-serif;
  }
  
  .post-list {
    list-style: none;
    padding: 0;
    margin-bottom: 20px;
  }
  
  .post-list li {
    margin: 12px 0;
    padding: 15px;
    background: #fff;
    border: 1px solid #ddd;
    border-radius: 5px;
    box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
    transition: background 0.3s ease-in-out;
  }
  
  .post-list li:hover {
    background: #f0f8ff;
  }
  
  .pagination-controls {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-top: 15px;
  }
  
  button {
    padding: 10px 20px;
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
  
  button:disabled {
    background-color: #ccc;
    cursor: not-allowed;
  }
  
  @media (max-width: 600px) {
    .pagination-container {
      padding: 15px;
    }
  
    .post-list li {
      padding: 12px;
      font-size: 0.9rem;
    }
  
    button {
      padding: 8px 16px;
    }
  }
  </style>
  
<!-- views/AlbumDetail.vue -->

<template>
    <div class="container">
        
        <nav aria-label="breadcrumb text-right">
            <ol class="breadcrumb ">
                <li class="breadcrumb-item"><a href="/">Home</a></li>
                <li class="breadcrumb-item active" aria-current="page">Albums Detail</li>
            </ol>
        </nav>

      <h3>Album Detail</h3>

      <div class="col-md-6 offset-md-3 mb-5">
        <div class="card mt-3">
            <img :src="album.url" :alt="album.title" class="card-img-top" width="200px">
            <div class="card-body text-center">
                <h5 class="card-title text-capitalize">{{ album.title }}</h5>
                <p class="card-text">{{ album.description }}</p>
                <router-link :to="{ name: 'Albums' }" class="btn btn-primary">
                    Back to Albums
                </router-link>
            </div>
        </div>
      </div>
    </div>

  </template>
  
  <script>
  import axios from 'axios';
  
  export default {
    props: ['id'],
    data() {
      return {
        album: null,
      };
    },
    created() {
      this.fetchAlbum();
    },
    methods: {
      async fetchAlbum() {
        try {
          const response = await axios.get(`https://jsonplaceholder.typicode.com/photos/${this.id}`);
          this.album = response.data;
        } catch (error) {
          console.error('Error fetching album:', error);
        }
      },
    },
  };
  </script>
  
  <style scoped>
  /* styles go here */
  </style>
  
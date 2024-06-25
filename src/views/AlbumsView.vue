<template>
    <div class="container">

        <nav aria-label="breadcrumb text-right">
        <ol class="breadcrumb ">
            <li class="breadcrumb-item"><a href="/">Home</a></li>
            <li class="breadcrumb-item active" aria-current="page">Albums</li>
        </ol>
        </nav>

        <!-- Isi Konten -->
        <div class="card">
            <div class="card-body">
                
                <h3 class="mb-5">Albums</h3>

                <div class="row grid">

                    <div class="col-2 text-center" v-for="album in albums" :key="album.id">
                        
                        <router-link :to="{ name: 'AlbumDetail', params: { id: album.id } }">
                            <img :src="album.thumbnailUrl" class="rounded  " alt="Album">
                        </router-link>
                        <p class="text-capitalize">{{ album.title }}</p>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import axios from 'axios';
    export default {
        data() {
            return {
                albums: [],
                selectedUser: null,
            };
        },
        created() {
            this.fetchAlbums();
        },
        methods: {
        async fetchAlbums() {
            try {
                const response = await axios.get('https://jsonplaceholder.typicode.com/photos?_limit=50');
                this.albums = response.data;
            } catch (error) {
                console.error('Error fetching albums:', error);
            }
        },
        },
    };
</script>


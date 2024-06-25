<template>
  <div class="container">

    <nav aria-label="breadcrumb text-right">
      <ol class="breadcrumb">
        <li class="breadcrumb-item"><a href="/">Home</a></li>
        <li class="breadcrumb-item active" aria-current="page">Post</li>
      </ol>
    </nav>

    <!-- Isi Konten -->
    <div class="card">
      <div class="card-body">
        
        <h3>Page Posts</h3>

        <div class="card mt-5 col-md-8 offset-lg-2">
          <div class="card-body">
            <div class="row g-2 mb-4">
              
              <label for="user-select" class="col-lg-2 col-form-label col-form-label-xl"><b>CHECK USERS</b></label>

              <div class="col-lg-7">
                <select class="form-control" id="user-select" v-model="selectedUserId" @change="fetchPosts" placeholder="-- Pilih Data Users --">
                  <option value="" selected hidden disabled>-- Pilih Data Users --</option>
                  <option v-for="user in users" :key="user.id" :value="user.id">{{ user.name }}</option>
                </select>
              </div>

              <div class="col-lg-3">
                <button type="submit" class="btn btn-primary m-1">Check</button>
                <button type="button" class="btn btn-warning" @click="resetForm">Reset</button>
              </div>
            </div>

            <hr>

            <!-- Menampilkan nama pengguna yang dipilih -->
            <div class="posts" v-if="selectedUser">
              <div>
                <label for="user-select">Data Post User : {{ selectedUser.name }}</label>
              </div>

              <table class="table table-bordered mt-3">
                <tbody>
                  <template v-for="post in posts" :key="post.id">                    
                    <tr>
                      <td>
                        <b class="text-uppercase">{{ post.title }}</b><br>
                        {{ post.body }}
                      </td>
                    </tr>
                    <tr>
                      <td class="text-center bg-light"></td>
                    </tr>
                  </template>
                </tbody>
              </table>
            </div>
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
      users: [],
      selectedUserId: null,
      selectedUser: null,
      posts: [],
    };
  },
  created() {
    this.fetchUsers();
  },
  methods: {
    async fetchUsers() {
      try {
        const response = await axios.get('https://jsonplaceholder.typicode.com/users');
        this.users = response.data;
      } catch (error) {
        console.error('Error fetching users:', error);
      }
    },
    async fetchPosts() {
      if (this.selectedUserId) {
        try {
          const response = await axios.get(`https://jsonplaceholder.typicode.com/posts?userId=${this.selectedUserId}`);
          this.posts = response.data;
          this.selectedUser = this.users.find(user => user.id === this.selectedUserId); // Update selectedUser
        } catch (error) {
          console.error('Error fetching posts:', error);
        }
      }
    },
    resetForm() {
      this.selectedUserId = null;
      this.selectedUser = null;
      this.posts = [];
    },
  },
};
</script>

<style scoped>
/* styles go here */
</style>

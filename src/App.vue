<template>
  <!-- Menu Navigation Bar -->
  <nav class="navbar navbar-expand-lg text-white" style="background-color: #7776b3">
    <div class="container-fluid">
      <a class="navbar-brand" href="/">
        <img
          src="/public/logotugas.png"
          alt="Logo"
          width="60"
          height="48"
          class="d-inline-block align-text-top"
        />
      </a>
      <button
        class="navbar-toggler"
        type="button"
        data-bs-toggle="collapse"
        data-bs-target="#navbarSupportedContent"
        aria-controls="navbarSupportedContent"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <ul class="navbar-nav me-auto mb-2 mb-lg-0">
          <li class="nav-item">
            <a class="nav-link text-white" aria-current="page" href="/">Home</a>
          </li>

          <li class="nav-item">
            <a class="nav-link text-white" aria-current="page" href="/todos">Todos</a>
          </li>

          <li class="nav-item">
            <a class="nav-link text-white" aria-current="page" href="/posts">Post</a>
          </li>

          <li class="nav-item">
            <a class="nav-link text-white" aria-current="page" href="/albums">Album</a>
          </li>
        </ul>

        <form class="d-flex" role="search">
          <input
            class="form-control me-2"
            type="search"
            placeholder="Cari..."
            aria-label="Search"
          />
          <button class="btn btn-outline-light" type="submit">Pencarian</button>
        </form>
      </div>
    </div>
  </nav>

  <!-- Konten Halaman Dashboard -->
  <div class="container mt-5">
    <div class="jumbotron" v-if="shouldShowJumbotron">
      <h1 class="display-4">Fiere Maulana</h1>
      <p class="lead">Tugas PBK</p>
      <hr class="my-4" />
      <p>
        Lorem ipsum dolor sit amet consectetur adipisicing elit. Magni doloribus molestiae, beatae
        hic sed error tempora debitis fuga dignissimos consectetur, velit quasi impedit qui quaerat
        et reprehenderit consequatur voluptatum inventore quas fugit. Vitae mollitia est modi omnis
        itaque molestias repellendus amet atque molestiae, doloribus sit! Aliquam commodi fugit
        nostrum vitae odio doloremque assumenda inventore ea amet fuga corporis quam, sequi dolore
        atque ullam, laboriosam beatae aspernatur ducimus blanditiis! At, fugiat qui? Provident
        cupiditate ipsa, nulla aspernatur reiciendis commodi maiores. Porro veritatis consectetur
        magnam sed at hic quas aliquam ut neque! Quia omnis voluptas, repudiandae veritatis quaerat
        atque expedita dolorum aliquid.
      </p>
      <a class="btn btn-primary btn-lg" href="#" role="button">Selengkapnya</a>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newActivity: '',
      activities: [],
      filter: 'all'
    }
  },
  methods: {
    addActivity() {
      if (this.newActivity.trim() !== '') {
        this.activities.push({ name: this.newActivity, completed: false })
        this.newActivity = ''
      }
    },
    cancelActivity(index) {
      this.activities.splice(index, 1)
    },
    showAll() {
      this.filter = 'all'
    },
    showPending() {
      this.filter = 'pending'
    },
    showCompleted() {
      this.filter = 'completed'
    }
  },
  computed: {
    filteredActivities() {
      if (this.filter === 'pending') {
        return this.activities.filter((activity) => !activity.completed)
      } else if (this.filter === 'completed') {
        return this.activities.filter((activity) => activity.completed)
      } else {
        return this.activities
      }
    },
    shouldShowJumbotron() {
      // Show jumbotron if not on the root path '/'
      return this.$route.path == '/'
    }
  }
}
</script>

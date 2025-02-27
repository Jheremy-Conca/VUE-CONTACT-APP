<template>
  <nav class="navbar navbar-expand-lg custom-navbar">
    <div class="container">
      <a class="navbar-brand text-light fw-bold" href="#">{{ title }}</a>
      <button
        class="navbar-toggler"
        type="button"
        data-bs-toggle="collapse"
        data-bs-target="#navbarNavAltMarkup"
        aria-controls="navbarNavAltMarkup"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarNavAltMarkup">
        <div class="navbar-nav ms-auto">
          <router-link class="nav-item nav-link" to="/">Home</router-link>
          <router-link class="nav-item nav-link" to="/create-contact">Create Contact</router-link>
        </div>
      </div>
    </div>
  </nav>
</template>

<script setup>
const props = defineProps({
  title: {
    type: String,
    required: true
  }
});
</script>

<style scoped>
.custom-navbar {
  background: #212529;
  padding: 10px 20px;
  border-bottom: 3px solid #0d6efd;
}

.navbar-brand {
  font-size: 1.5rem;
  transition: color 0.3s;
}

.navbar-brand:hover {
  color: #0d6efd;
}

.navbar-nav .nav-link {
  color: #adb5bd;
  font-weight: 500;
  margin-right: 15px;
  transition: color 0.3s;
}

.navbar-nav .nav-link:hover {
  color: #ffffff;
}

.navbar-nav .nav-link.router-link-active {
  color: #0d6efd;
  font-weight: bold;
}
</style>

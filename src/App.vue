<script setup>
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <header>
    <div class="wrapper">
      <nav class="navbar navbar-expand-lg nav-dark bg-dark">
        <div class="container">
          <RouterLink class="navbar-brand text-white" to="/">Navbar</RouterLink>
          <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
            <span class="navbar-toggler-icon text-white"></span>
          </button>
          <div class="collapse navbar-collapse" id="navbarSupportedContent">
            <ul class="navbar-nav ms-auto mb-2 mb-lg-0">
              <li class="nav-item">
                <RouterLink class="nav-link active text-white" to="/">Home</RouterLink>
              </li>
              <li class="nav-item">
                <RouterLink class="nav-link active text-white" to="/about">About</RouterLink>
              </li>
              <li class="nav-item">
                <RouterLink class="nav-link active text-white" to="/student">Student</RouterLink>
              </li>
            </ul>
          </div>
        </div>
      </nav>
    </div>
  </header>

  <RouterView />
</template>

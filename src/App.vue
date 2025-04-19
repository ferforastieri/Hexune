<script setup>
import Header from './components/layout/Header.vue'
import Hero from './components/sections/Hero.vue'
import Articles from './components/sections/Articles.vue'
</script>

<template>
  <Header />
  <main>
    <Hero />
    <Articles />
  </main>
</template>

<style>
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap');

:root {
  --primary-color: #42b883;
  --secondary-color: #2c3e50;
  --text-color: #64748b;
  --background-color: #ffffff;
  --gradient-primary: linear-gradient(45deg, var(--secondary-color), var(--primary-color));
  --gradient-secondary: linear-gradient(45deg, var(--primary-color), var(--secondary-color));
}

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: 'Inter', sans-serif;
  line-height: 1.6;
  color: var(--text-color);
  background-color: var(--background-color);
}

a {
  text-decoration: none;
  color: inherit;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 2rem;
}

section {
  padding: 5rem 0;
}

@media (max-width: 768px) {
  section {
    padding: 3rem 0;
  }
}
</style>

<script setup>
  import Navbar from './components/Navbar.vue'
  import Landing from './components/Landing.vue'
  import About from './components/About.vue'
  import Skills from './components/Skills.vue'
  import Projects from './components/Projects.vue'
  import Experience from './components/Experience.vue'
  import Contact from './components/Contact.vue'
  import Footer from './components/Footer.vue'
</script>

<template>
<Navbar />
<div class="container">
  <Landing />
  <About />
  <Skills />
  <Projects />
  <Experience />
  <Contact />
</div>
<Footer />
</template>

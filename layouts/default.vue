<template>
  <div>
    <Navbar/>
    <!-- аналог vue router, сюда рендерятся компоненеты страницы -->
    <Nuxt />
  </div>
</template>

<script>
import Navbar from '../components/Navbar/Navbar.vue';
export default {
  components: {
    Navbar
  }
}
</script>


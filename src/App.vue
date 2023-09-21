<script setup>
import { RouterLink, RouterView } from 'vue-router'
import HelloWorld from './components/HelloWorld.vue'
</script>

<template>
 
      <nav>
        <RouterLink to="/" class="btn btn-primary mr-3">Home</RouterLink>
        <RouterLink to="/Product" class="btn btn-primary">Product List </RouterLink>
      </nav>
    
  <RouterView />
</template>

<style scoped>
</style>

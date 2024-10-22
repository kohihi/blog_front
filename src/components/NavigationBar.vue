<script setup lang="ts">
  import { ref, computed } from 'vue'
  import Home from './PageHome.vue'
  import ACGNM from './PageACGNM.vue'
  import Article from './PageArticle.vue'

  const routes = {
    '/': Home,
    '/acgnm': ACGNM,
    '/article': Article
  }

  const currentPath = ref(window.location.hash)
  window.addEventListener('hashchange', () => {
    currentPath.value = window.location.hash
  })
  const currentView = computed(() => {
    return routes[currentPath.value.slice(1) || '/'] || NotFound
  })
</script>

<template>
    <a href="#/">Home</a> |
    <a href="#/acgnm">A·C·G·N·M</a>
    <div>
      <component :is="currentView" />
    </div>
</template>
  
<style scoped>
</style>
  
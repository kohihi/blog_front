<script setup lang="ts">
import { ref, computed } from 'vue'
import Home from './components/PageHome.vue'
import ACGNM from './components/PageACGNM.vue'
import Article from './components/PageArticle.vue'
import Editor from './components/PageEditor.vue'
import Admin from './components/PageAdmin.vue'

const routes: Record<string, any> = {
    '/': Home,
    '/acgnm': ACGNM,
    '/article': Article,
    '/editor': Editor,
    '/admin': Admin,
  }

  const currentPath = ref<string>(window.location.hash)
  window.addEventListener('hashchange', () => {
    currentPath.value = window.location.hash
  })
  const currentView = computed(() => {
    let route: string | undefined = currentPath.value.slice(1)
    route = currentPath.value.slice(1) || '/'
    if (route == '/'){
      return Home
    } else {
      route = '/' + route.split('/', 2)[1]
      return routes[route] // NotFound 页面
    }
  })
</script>

<template>
    <a href="#/">Home</a> |
    <a href="#/acgnm">A·C·G·N·M</a> |
    <a href="#/editor">Editor</a> |
    <a href="#/admin">后台</a>
    <div>
      <component :is="currentView" />
    </div>
</template>
  
<style scoped>
</style>
<script setup lang="ts">
import { ref, computed } from 'vue'
import Home from './components/PageHome.vue'
import ACGNM from './components/PageACGNM.vue'
import Article from './components/PageArticle.vue'
import Editor from './components/PageEditor.vue'
import Admin from './components/PageAdmin.vue'
import Record from './components/PageRecord.vue'

const routes: Record<string, any> = {
    '/': Home,
    '/acgnm': ACGNM,
    '/article': Article,
    '/admin': Admin,
    '/editor': Editor,
    '/record': Record,
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
  <div class="bgWrap"></div>
  <!-- <div class="header"></div> -->
  <div style="display: block;">
    <a href="#/">Blog</a> |
    <a href="#/acgnm">A·C·G·N·M</a>
  </div>
  <component :is="currentView" />
</template>
  
<style scoped>
.header{
  width: 100vw;
  height: 48px;
  background: url(/src/assets/site_header.png) no-repeat center;
  background-color: #fff;
  box-shadow: 0px 2px 2px #ffffff;
  margin-bottom: 10px;
  font-size: 32px;
  filter: brightness(0.7);
  position: fixed;
  left: 0px;
  top: 0px;
}

.bgWrap {
  width: 100%;
  height: 100%;
  background-image: url(/src/assets/texture.png);
  background-color: #fffef9;
  position: fixed;
  z-index: -1;
  position: fixed;
  left: 0px;
  top: 0px;
}
</style>
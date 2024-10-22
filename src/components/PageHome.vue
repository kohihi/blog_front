<script setup lang="ts">
  import { ref, computed } from 'vue'
  import axios from 'axios'
  import Home from './PageHome.vue'
  import ACGNM from './PageACGNM.vue'
  import Article from './PageArticle.vue'
  import ArticleItem from './ArticleItem.vue'

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

  let emp = ref([])
  axios.get('http://127.0.0.1:9911/article/')
    .then(function (response) {
      // 处理成功情况
      emp.value = response.data.data;
    })
    .catch(function (error) {
      // 处理错误情况
      console.log(error);
    })
    .finally(function () {
      // 总是会执行
    });
</script>

<template>
  <ArticleItem 
    v-for="item in emp"
    :apiHref="'http://127.0.0.1:9911/article/' + item._id">
    <template #title>{{ item.title }}</template>
    <template #summary>{{ item.summary }}</template>
  </ArticleItem>
</template>
  
<style scoped>
  .item {
    margin-top: 2rem;
    display: block;
    position: relative;
  }
  
  .title {
    flex: 1;
    margin-left: 1rem;
  }

  .summary {
    flex: 1;
    margin-left: 1rem;
  }
  
  i {
    display: flex;
    place-items: center;
    place-content: center;
    width: 32px;
    height: 32px;
  
    color: var(--color-text);
  }
  
  h3 {
    font-size: 1.2rem;
    font-weight: 500;
    margin-bottom: 0.4rem;
    color: var(--color-heading);
  }
  
  @media (min-width: 1024px) {
    .item {
      margin-top: 0;
      padding: 0.4rem 0 1rem calc(var(--section-gap) / 2);
    }
  
    i {
      top: calc(50% - 25px);
      left: -26px;
      position: absolute;
      border: 1px solid var(--color-border);
      background: var(--color-background);
      border-radius: 8px;
      width: 50px;
      height: 50px;
    }
  
    .item:before {
      content: ' ';
      border-left: 1px solid var(--color-border);
      position: absolute;
      left: 0;
      bottom: calc(50% + 25px);
      height: calc(50% - 25px);
    }
  
    .item:after {
      content: ' ';
      border-left: 1px solid var(--color-border);
      position: absolute;
      left: 0;
      top: calc(50% + 25px);
      height: calc(50% - 25px);
    }
  
    .item:first-of-type:before {
      display: none;
    }
  
    .item:last-of-type:after {
      display: none;
    }
  }
  </style>
  
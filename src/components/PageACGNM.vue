<script setup lang="ts">
import CradItem from "./ACGNMItem.vue"
import { ref, computed } from 'vue'
import axios from 'axios'

let anime = ref([])
let game = ref([])
let movie = ref([])
let book = ref([])

// 滚动到指定的 H3 元素
const scrollToSection = (section: string) => {
  const target = document.getElementById(section)
  if (target) {
    target.scrollIntoView({ behavior: 'smooth' }) // 平滑滚动
  }
}

// 回到顶部
const scrollToTop = () => {
  window.scrollTo({
    top: 0,
    behavior: 'smooth' // 使用平滑滚动
  });
};

axios.get('http://127.0.0.1:9911/acgnm/',
  {
    params: {
      board: "anime"
    }
  })
  .then(function (response) {
    // 处理成功情况
    anime.value = response.data.data;
  })
  .catch(function (error) {
    // 处理错误情况
    console.log(error);
  })
  .finally(function () {
    // 总是会执行
  });

axios.get('http://127.0.0.1:9911/acgnm/',
  {
    params: {
      board: "game"
    }
  })
  .then(function (response) {
    // 处理成功情况
    game.value = response.data.data;
  })
  .catch(function (error) {
    // 处理错误情况
    console.log(error);
  })
  .finally(function () {
    // 总是会执行
  });

axios.get('http://127.0.0.1:9911/acgnm/',
  {
    params: {
      board: "movie"
    }
  })
  .then(function (response) {
    // 处理成功情况
    movie.value = response.data.data;
  })
  .catch(function (error) {
    // 处理错误情况
    console.log(error);
  })
  .finally(function () {
    // 总是会执行
  });

axios.get('http://127.0.0.1:9911/acgnm/',
  {
    params: {
      board: "book"
    }
  })
  .then(function (response) {
    // 处理成功情况
    book.value = response.data.data;
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
  <div class="about">
    <h2>关于这个页面</h2>
    <p>自己喜欢的一些作品，在这里做个记录。也是做推荐，如果有人访问这个页面，也许就传教成功了也说不定。</p>
  </div>
  <div class="index">
    <li @click="scrollToSection('anime')">动画 ({{ anime.length }})</li>
    <li @click="scrollToSection('game')">游戏 ({{ game.length }})</li>
    <li @click="scrollToSection('movie')">电影 ({{ movie.length }})</li>
    <li @click="scrollToSection('book')">书籍 ({{ book.length }})</li>
    <li @click="scrollToTop">↑↑↑ </li>
  </div>

  <h3 id="anime">动画</h3>
  <div class="board-set">
    <CradItem 
      v-for="item in anime"
      :imgSrc="item.cover"
      :outLink="item.link"
      >
      <template #title>{{ item.title }}</template>
    </CradItem>
  </div>

  <h3 id="game">游戏</h3>
  <div class="board-set">
    <CradItem 
    v-for="item in game"
    :imgSrc="item.cover"
    :outLink="item.link"
    >
    <template #title>{{ item.title }}</template>
    </CradItem>
  </div>

  <h3 id="movie">电影</h3>
  <div class="board-set">
    <CradItem 
    v-for="item in movie"
    :imgSrc="item.cover"
    :outLink="item.link"
    >
    <template #title>{{ item.title }}</template>
    </CradItem>
  </div>

  <h3 id="book">书籍</h3>
  <div class="board-set">
    <CradItem 
    v-for="item in book"
    :imgSrc="item.cover"
    :outLink="item.link"
    >
    <template #title>{{ item.title }}</template>
    </CradItem>
  </div>
</template>
  
<style scoped>
.index{
  position: fixed;
  right: 1rem;
  top: 3rem;
  font-size: 16px;
}
.index li {
  cursor: pointer;
  color: green;
}
h3 {
  font-size: 1.3rem;
}
</style>
  
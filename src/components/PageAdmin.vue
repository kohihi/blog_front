<script setup lang="ts">
import { ref } from 'vue'
import axios from 'axios'
import AdminArticleItem from './AdminAriticleItem.vue'
import AdminCardItem from './AdminACGNMItem.vue'

// 文章列表获取
let article = ref([{
  _id: "",
  title: "",
  summary: "",
  ct: "",
  ut: "",
}])

axios.get('http://127.0.0.1:9911/article/')
  .then(function (response) {
    // 处理成功情况
    article.value = response.data.data;
  })
  .catch(function (error) {
    // 处理错误情况
    console.log(error);
  })
  .finally(function () {
    // 总是会执行
  });

// 记录列表获取
let anime = ref([{
  _id: "",
  board: "",
  title: "",
  summary: "",
  cover: "",
  link: "",
  ct: "",
  ut: "",
}])
let game = ref([{
  _id: "",
  board: "",
  title: "",
  summary: "",
  cover: "",
  link: "",
  ct: "",
  ut: "",
}])
let movie = ref([{
  _id: "",
  board: "",
  title: "",
  summary: "",
  cover: "",
  link: "",
  ct: "",
  ut: "",
}])
let book = ref([{
  _id: "",
  board: "",
  title: "",
  summary: "",
  cover: "",
  link: "",
  ct: "",
  ut: "",
}])

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

// 默认展示文章列表
let showArticle = ref(true)
let showRecord = ref(false)


function showRecordView() {
  showArticle.value = false
  showRecord.value = true
}

function showArticleView() {
  showArticle.value = true
  showRecord.value = false
}
</script>

<template>
  <title>FUE</title>
  <h1>后台</h1>
  <button @click="showArticleView">文章列表</button>
  <button @click="showRecordView">记录列表</button>

<div v-if="showArticle">
  <a href="#/editor">新增文章</a>
  <AdminArticleItem 
    v-for="item in article"
    :articleViewHref="'#/article/' + item._id"
    :articleEditorHref="'#/editor/' + item._id">
    <template #date>{{ item.ct }}</template>
    <template #title>{{ item.title }}</template>
    <template #summary>{{ item.summary }}</template>
  </AdminArticleItem>
</div>

<div v-if="showRecord">
  <a href="#/record">新增记录</a>
  <span class="board">动画</span>
  <div class="board-set">
    <AdminCardItem 
      v-for="item in anime"
      :imgSrc="item.cover"
      :outLink="item.link"
      :editorLink="'#/record/' + item._id"
      >
      <template #title>{{ item.title }}</template>
      <template #summary>{{ item.summary }}</template>
    </AdminCardItem>
  </div>
  <span class="board">游戏</span>
  <div class="board-set">
    <AdminCardItem 
    v-for="item in game"
    :imgSrc="item.cover"
    :outLink="item.link"
    :editorLink="'#/record/' + item._id"
    >
    <template #title>{{ item.title }}</template>
    <template #summary>{{ item.summary }}</template>
  </AdminCardItem>
  </div>

  <span class="board">电影</span>
  <div class="board-set">
    <AdminCardItem 
    v-for="item in movie"
    :imgSrc="item.cover"
    :outLink="item.link"
    :editorLink="'#/record/' + item._id"
    >
    <template #title>{{ item.title }}</template>
    <template #summary>{{ item.summary }}</template>
  </AdminCardItem>
  </div>

  <span class="board">书籍</span>
  <div class="board-set">
    <AdminCardItem 
    v-for="item in book"
    :imgSrc="item.cover"
    :outLink="item.link"
    :editorLink="'#/record/' + item._id"
    >
    <template #title>{{ item.title }}</template>
    <template #summary>{{ item.summary }}</template>
  </AdminCardItem>  </div>

</div>

</template>
  
<style scoped>
.board {
  font-size: 1.2rem;
  display: block;
}

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
  
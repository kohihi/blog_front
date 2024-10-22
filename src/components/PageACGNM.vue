<script setup lang="ts">
import CradItem from "./ACGNMItem.vue"
import { ref, computed } from 'vue'
import axios from 'axios'

let anime = ref([])
let game = ref([])
let movie = ref([])
let book = ref([])

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
  <h3>动画</h3>
  <CradItem 
    v-for="item in anime"
    :imgSrc="item.cover"
    :outLink="item.link"
    >
    <template #title>{{ item.title }}</template>
  </CradItem>
  <h3>游戏</h3>
  <CradItem 
    v-for="item in game"
    :imgSrc="item.cover"
    :outLink="item.link"
    >
    <template #title>{{ item.title }}</template>
  </CradItem>
  <h3>电影</h3>
  <CradItem 
    v-for="item in movie"
    :imgSrc="item.cover"
    :outLink="item.link"
    >
    <template #title>{{ item.title }}</template>
  </CradItem>
  <h3>书籍</h3>
  <CradItem 
    v-for="item in book"
    :imgSrc="item.cover"
    :outLink="item.link"
    >
    <template #title>{{ item.title }}</template>
  </CradItem>

</template>
  
<style scoped>
</style>
  
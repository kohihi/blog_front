<script setup lang="ts">
  import { ref } from 'vue'
  import axios from 'axios'
  import ArticleItem from './ArticleItem.vue'



  let article = ref([{
    _id: "",
    title: "",
    summary: "",
    header: "",
    views: 0,
    tag: "",
    ct: "",
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
</script>

<template>
<div class="articleList">
  <ArticleItem 
    v-for="item in article"
    :apiHref="'#/article/' + item._id"
    :header="item.header">
    <template #title>{{ item.title }}</template>
    <template #summary>{{ item.summary }}</template>
    <template #views>{{ item.views }}</template>
    <template #tag>{{ item.tag }}</template>
    <template #ct>{{ item.ct }}</template>
  </ArticleItem>
</div>
</template>
  
<style scoped>

.articleList {
  display: flex;
  flex-wrap: wrap;
}

</style>
  
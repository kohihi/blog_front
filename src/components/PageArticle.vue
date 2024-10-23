<script setup lang="ts">
import { ref } from 'vue'
import axios from 'axios'
import { marked } from 'marked'

const article_id: string = window.location.hash.split('/').slice(-1)[0]
const article = ref({
  title: "",
  content: "",
})
const content_html = ref<string | Promise<string>>("Article Content")



axios.get('http://127.0.0.1:9911/article/' + article_id)
  .then(function (response) {
    // 处理成功情况
    article.value = response.data.data;
    content_html.value = marked.parse(article.value.content)
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
  <h1>{{ article.title }}</h1>
  <hr>
  <span v-html="content_html"></span>
</template>
  
<style scoped>
</style>
  
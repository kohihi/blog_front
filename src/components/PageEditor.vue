<script setup lang="ts">
import { ref, computed} from 'vue'
import { marked } from 'marked'
import { debounce } from 'lodash-es'
import axios from 'axios'
import globle_ from './globle.vue'


// 输入预览处理
const input = ref('### **没有**实时保存，建议在本地编辑器写好再复制到这里')
const contentHtml = computed(() => marked(input.value))
const update = debounce((e) => {input.value = e.target.value}, 100)

const article = ref({
  title: "",
  content: "",
  summary: "",
  header: "",
  tag: "",
  _id: "",
})

// 修改文章加载文章内容
const article_id: string = window.location.hash.split('/').slice(-1)[0]
if (article_id != 'editor') {
  axios.get(globle_.apiArticle + article_id)
    .then(function (response) {
      // 处理成功情况
      article.value = response.data.data;
      input.value = article.value.content
    })
    .catch(function (error) {
      // 处理错误情况
      console.log(error);
    })
    .finally(function () {
      // 总是会执行
    });
}

function submitArticle() {
  article.value.content = input.value
  axios.post(globle_.apiArticle, article.value)
    .then(function (response) {
      // 处理成功情况
    })
    .catch(function (error) {
      // 处理错误情况
      console.log(error);
    })
    .finally(function () {
      // 总是会执行
    });
}
</script>

<template>
<h1>编辑器</h1>
<hr>

<h2>标题：<input type="text" name="title" placeholder="不得为空" v-model="article.title"></h2>
<div>{{ article._id }}</div>
<p>题图：<input type="text" name="header" v-model="article.header"></p>
<p>简介：<input type="text" name="summary" v-model="article.summary"></p>
<p>标签：<input type="text" name="tag" placeholder="xxx/xxx/xxx" v-model="article.tag"></p>
<div class="editor">
  <textarea class="input" v-model="input" @input="update"></textarea>
  <div class="contentPrivew" v-html="contentHtml"></div>
</div>


<button class="submit" @click="submitArticle">提交</button>
</template>
  
<style>
  .editor {
    height: 70vh;
    display: flex;
  }
  .input,
  .contentPrivew {
    overflow: auto;
    width: 50%;
    height: 100%;
    box-sizing: border-box;
    padding: 0px 20px;
    border: 1px solid #ccc;
  }
  .input {
    color: var(--color-text);
    background: var(--color-background);
    resize: none;
    outline: none;
    padding: 20px;
    color: (235, 235, 235);
  }
  .submit {
    margin: 10px 0;
    width: 100%;
    height: 40px;
    color: var(--color-text);
    background: #797ca3;
  }
  code {
    color: green;
  }
  p {
    margin: 3px 0;
  }
</style>
  
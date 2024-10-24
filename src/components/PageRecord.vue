<script setup lang="ts">
import { ref } from 'vue'
import axios from 'axios'
import globle_ from './globle.vue'


// 输入预览处理
const record = ref({
  board: "",
  title: "",
  summary: "",
  cover: "",
  link: "",
  _id: "",
})

// 修改 Record 加载内容
const recordId: string = window.location.hash.split('/').slice(-1)[0]
if (recordId != 'record') {
  axios.get(globle_.apiRecord + recordId)
    .then(function (response) {
      // 处理成功情况
      record.value = response.data.data;
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
  axios.post(globle_.apiRecord, record.value)
    .then(function (response) {
      // 处理成功情况
			alert("提交完成")
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
<h1>Record</h1>
<hr>
<div>{{ record._id }}</div>
<h2>标题：<input type="text" name="title" placeholder="不得为空" v-model="record.title"></h2>
<p>海报：<input type="text" name="header" v-model="record.cover"></p>
<img :src="record.cover" class="cover" alt="">
<p>一句话：<input type="text" name="summary" v-model="record.summary"></p>
<p>类型：
	<select name="board" id="" v-model="record.board">
		<option value="anime">动画</option>
		<option value="game">游戏</option>
		<option value="movie">电影</option>
		<option value="book">书籍</option>
	</select>
</p>
<p>外链：<input type="text" name="tag" placeholder="跳转链接" v-model="record.link"></p>
<button class="submit" @click="submitArticle">提交</button>
</template>
  
<style>
.cover {
	width: 120px;
	height: 160px;
}

.submit {
  margin: 10px 0;
	width: 100%;
	height: 40px;
	color: var(--color-text);
	background: #797ca3;
}

p {
	margin: 3px 0;
}
</style>
  
<script setup lang="ts">
import CradItem from "./ACGNMItem.vue"
import { ref, computed } from 'vue'
import axios from 'axios'

let article = ref({})

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
  <p>
    {{ article.content }}
  </p>
</template>
  
<style scoped>
</style>
  
<script setup lang="ts">
const props = defineProps<{
  apiHref: string
  header: string
}>()

const openArticle = () => {
  window.location.href = props.apiHref;
}

</script>

<template>
<div class="item" @click="openArticle">
  <div class="articleInfo">
    <div class="title">
      <h3>
        <a :href="apiHref">
          <slot name="title">defaule title</slot>
        </a>
      </h3>
    </div>
    <div class="summary">
      <p>
        <slot name="summary">default summary</slot>
      </p>
      <p>
        <slot name="tag">0</slot>
      </p>
      <p>
        发布时间：<slot name="ct">2000-01-01 00:00:00</slot>
      </p>
      <p>
        浏览：<slot name="views">0</slot>
      </p>
    </div>
  </div>
  <div class="background" :style="{'background': `url(${header})`, 'background-size': 'cover'}"></div>
</div>
</template>
  
<style scoped>

.background{
  width: 100%;
  height: 100%;
  background-size: cover;
  opacity: 1;
  filter: blur(3px);
  z-index: 1;
}
.background::after{
  content: "";
  background: white;
  opacity: 0.7;
  position: absolute;
  width: 100%;
  height: 100%;
}
.articleInfo{
  position: absolute;
  z-index: 2;
}

.item {
  display: flex;
  width: 550px;
  height: 150px;
  margin-top: 1rem;
  margin-left: 1rem;
  position: relative;
  border: 1px solid green;
  cursor: pointer;
  transition: transform 0.2s ease; /* 添加平滑过渡效果 */
}

.item:hover {
  transform: scale(1.05); /* 鼠标悬停时放大 1.1 倍 */
}

.item a {
  background-color: transparent; /* 确保背景颜色为透明 */
}

.item a:hover {
  background-color: transparent; /* 悬停时背景颜色仍为透明 */
  text-decoration: none; /* 可选：去掉下划线 */
}

.title {
  flex: 1;
  margin-left: 1rem;
  z-index: 2;
}

.summary {
  flex: 1;
  margin-left: 1rem;
  z-index: 2;
}

h3 {
  font-size: 1.1rem;
  font-weight: 500;
  margin-bottom: 0.4rem;
  color: var(--color-heading);
}

</style>
  
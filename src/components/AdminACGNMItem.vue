<script setup lang="ts">
const props = defineProps<{
  imgSrc: string,
  outLink: string,
  editorLink: string,
}>()
</script>

<template>
  <div class="card">
    <div class="cover">
      <img :src="imgSrc" alt="cover">
    </div>
    <div class="card-text">
      <a :href="outLink" target="_blank">
        <slot name="title">
          作品标题
        </slot>
      </a>
      <slot name="summary">一句话</slot>
      <a :href="editorLink">编辑</a>
    </div>
  </div>
</template>
  
<style scoped>
  .card-text {
    display: block;
  }
  .card-text a {
    display: block;
  }
  .cover {
    width: 90px;
    height: 120px;
    border: 1px solid whitesmoke;
  }
  .card {
    display: flex;
    width: 360px;
    height: 120px;
    margin: 5px;
  }
  img {
    max-width: 100%;
    max-height: 100%;
  }

</style>
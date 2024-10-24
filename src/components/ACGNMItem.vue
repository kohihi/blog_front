<script setup lang="ts">
const props = defineProps<{
  imgSrc: string,
  outLink: string
}>()
</script>

<template>
  <div class="crad">
    <img class="cover" :src="imgSrc" alt="cover">
    <a :href="outLink">
      <slot name="title">
        作品标题
      </slot>
    </a>  
  </div>
</template>
  
<style scoped>
.crad {
  width: 200px;
  margin-right: 30px;
  margin-bottom: 20px;
}
.cover {
  width: 200px;
  height: auto;
}
</style>
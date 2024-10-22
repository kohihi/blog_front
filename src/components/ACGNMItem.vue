<script setup lang="ts">
import cradItem from "./ACGNMItem.vue"
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
    display: inline-block;
    width: 150px;
    margin: 5px;
  }
  .cover {
    width: 150px;
    height: 200px;
  }
</style>
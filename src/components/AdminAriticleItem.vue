<script setup lang="ts">
const props = defineProps<{
  articleViewHref: string
  articleEditorHref: string
}>()
</script>

<template>
<div class="item">
  <div class="date">
  @<slot name="date">1990-1-1</slot>
  </div>
  <div class="title">
    <a :href="articleViewHref">
    <slot name="title">defaule title</slot>
    </a>
    >>>>>><a class="editor" :href="articleEditorHref">编辑</a>
  </div>
  <div class="summary">
  <slot name="summary">default summary</slot>
  </div>

</div>
</template>
  
<style scoped>
.item {
  margin: 5px;
  padding: 5px;
}

.title {
  flex: 1;
  font-size: 1rem;
  margin-left: 1rem;
}

.summary {
  flex: 1;
  margin-left: 1rem;
}

.date {
  /* flex: 1; */
  font-size: 0.5rem;
  margin-left: 1rem;
}

.editor {
  display: inline;
  font-size: 0.5rem;
}

</style>
  
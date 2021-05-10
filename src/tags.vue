<script>
import Tag from './tag';

export default {
  name: 'Tags',
  components: {
    Tag,
  },
  data() {
    return {
      tags: [],
    };
  },
}
</script>

<template>
  <div class="tags-container">
    <tag v-for="(tag, index) in tags" :key="index" :content="tag" />
    <textarea class="tag-input" />
  </div>
</template>

<style scoped>
.tags-container {
  border: 1px solid #ccc;
  padding: 6px;
  display: flex;
  flex-wrap: wrap;
}

.tags-container .tag-input {
  outline: none;
  border: none;
  font-size: 16px;
  flex-grow: 1;
  resize: none;
  white-space: nowrap;
  overflow: hidden;
  width: 40px;
}
</style>

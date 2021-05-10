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
  methods: {
    addTag(event) {
      event.preventDefault(); // prevent cursor to create a new line in textarea

      const tag = event.target.value.trim();
      const existingTag = this.tags.find(t => t.toLowerCase() == tag.toLowerCase());

      if (existingTag) return;

      this.tags.push(tag);

      event.target.value = '';
    },
  }
}
</script>

<template>
  <div class="tags-container">
    <tag v-for="(tag, index) in tags" :key="index" :content="tag" />
    <textarea class="tag-input" @keydown.enter.exact="addTag" />
  </div>
</template>

<style scoped>
.tags-container {
  border: 1px solid #ccc;
  padding: 6px 6px 2px;
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

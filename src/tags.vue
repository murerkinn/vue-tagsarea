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
      textareaValue: '',
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
    removeTag(tagIndex) {
      if (tagIndex) return this.tags.splice(tagIndex, 1);

      if (!this.textareaValue) this.tags.splice(this.tags.length - 1, 1);
    }
  }
}
</script>

<template>
  <div class="tags-container">
    <span v-if="$scopedSlots.tag" v-for="(tag, index) in tags" :key="index">
      <slot name="tag" :content="tag" :index="index" :remove="removeTag"></slot>
    </span>

    <tag
      v-else
      v-for="(tag, index) in tags"
      :key="index"
      :content="tag"
      @remove="removeTag(index)"
    />

    <textarea v-model="textareaValue" class="tag-input" @keydown.enter.exact="addTag" @keydown.backspace="removeTag" />
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

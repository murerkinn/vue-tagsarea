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
      existingTagIndex: -1,
    };
  },
  props: {
    value: {
      type: [String, Array],
      required: false,
    },
    seperator: {
      type: String,
      required: false,
      default: '\n',
    },
    showRemoveAll: {
      type: Boolean,
      required: false,
      default: false,
    },
    theme: {
      type: String,
      validator: (value) => ['primary', 'secondary', 'success', 'danger', 'warning', 'info', 'light', 'dark'].indexOf(value.toLowerCase()) !== -1,
    },
  },
  watch: {
    tags() {
      this.$emit('input', (this.value && Array.isArray(this.value)) ? this.tags : this.tags.join(this.seperator));
    },
    textareaValue(val) {
      const regex = new RegExp(this.seperator, 'g');

      if (this.seperator && regex.test(val)) {
        this.tags = [...this.tags, ...(new Set(val.split(this.seperator)))];
        this.textareaValue = ''
      }
    },
    existingTagIndex(val) {
      if (val != -1)
        setTimeout(() => {
          this.existingTagIndex = -1;
        }, 600);
    }
  },
  methods: {
    addTag(event) {
      event.preventDefault(); // prevent cursor to create a new line in textarea

      const tag = event.target.value.trim();
      const existingTagIndex = this.tags.findIndex(t => t.toLowerCase() == tag.toLowerCase());

      if (!tag) return;

      if (existingTagIndex >= 0) {
        this.existingTagIndex = existingTagIndex;
        return;
      }

      const regex = new RegExp(this.seperator, 'g');

      if (this.seperator && regex.test(tag)) {
        this.tags = [...this.tags, ...(new Set(tag.split(this.seperator)))];
      } else this.tags.push(tag);
      event.target.value = '';
    },
    removeTag(tagIndex) {
      if (typeof tagIndex == 'number') {
        this.tags.splice(tagIndex, 1);
        this.$refs.tagsarea.focus();
        return;
      }

      if (!this.textareaValue) this.tags.splice(this.tags.length - 1, 1);
    },
    removeAllTags() {
      this.tags = [];
      this.$refs.tagsarea.focus();
    }
  },
  created() {
    this.tags = (this.value && Array.isArray(this.value)) ? this.value : this.value.split(this.seperator).filter((t) => t);
  }
}
</script>

<template>
  <div class="tags-container">
    <slot v-if="$scopedSlots.removeAllButton && tags.length > 1" name="removeAllButton" :removeAll="removeAllTags"></slot>

    <tag
      v-else-if="showRemoveAll && tags.length > 1"
      style="cursor: pointer"
      content="Remove all"
      @click.native="removeAllTags"
    />

    <span v-if="$scopedSlots.tag">
      <slot v-for="(tag, index) in tags" name="tag" :content="tag" :index="index" :remove="removeTag" :exists="existingTagIndex == index"></slot>
    </span>

    <tag
      v-else
      v-for="(tag, index) in tags"
      :key="index"
      :content="tag"
      :exists="existingTagIndex == index"
      :theme="theme"
      @remove="removeTag(index)"
    />

    <textarea ref="tagsarea" v-model="textareaValue" class="tag-input" @keydown.enter.exact="addTag" @keydown.backspace="removeTag" @keydown.enter.shift="(e) => e.preventDefault()" />
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
  font-size: 12px;
  line-height: 22px;
  flex-grow: 1;
  resize: none;
  white-space: nowrap;
  overflow: hidden;
  width: 40px;
  height: 24px;
  font-weight: 500;
}
</style>

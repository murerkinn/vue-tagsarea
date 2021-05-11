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
      existingTags: [],
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
    placeholder: {
      type: String,
      required: false,
      default: 'Enter your tags here...'
    }
  },
  watch: {
    tags() {
      this.$emit('input', (this.value && Array.isArray(this.value)) ? this.tags : this.tags.join(this.seperator));
    },
    existingTags(tags) {
      if (tags.length)
        setTimeout(() => {
          this.existingTags = [];
        }, 600);
    }
  },
  methods: {
    addTag(tag) {
      if(this.tags.find(t => t.toLowerCase() == tag.toLowerCase())) return this.existingTags.push(tag)

      this.tags.push(tag)
      this.textareaValue = ''
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
    },
    addTagWithEvent(event) {
      event.preventDefault(); // prevent cursor to create a new line in textarea

      let data;

      switch (event.type) {
        case 'keydown':
          data = event.target.value.trim()
          break;
       case 'paste':
          data = event.clipboardData.getData('text/plain').trim();
          break;
      }

      if (!data) return;

      const regex = new RegExp(this.seperator, 'g');

      if (this.seperator && regex.test(data)) {
        let tags = [...(new Set(data.split(this.seperator).filter(t => t).map(t => t.trim())))];

        tags.forEach(this.addTag)
      } else this.addTag(data)
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

    <!-- eslint-disable -->
    <span v-if="$scopedSlots.tag">
      <slot
        v-for="(tag, index) in tags"
        name="tag"
        :content="tag"
        :index="index"
        :remove="removeTag"
        :exists="existingTags.includes(tag)"
      ></slot>
    </span>

    <tag
      v-else
      v-for="(tag, index) in tags"
      :key="index"
      :content="tag"
      :exists="existingTags.includes(tag)"
      :theme="theme"
      @remove="removeTag(index)"
    />

    <textarea
      ref="tagsarea"
      v-model="textareaValue"
      class="tag-input"
      @keydown.enter.exact="addTagWithEvent"
      @keydown.backspace="removeTag"
      @keydown.enter.shift="e => e.preventDefault()"
      @paste="addTagWithEvent"
      :placeholder="!tags.length && placeholder"
    />
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

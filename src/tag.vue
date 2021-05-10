<script>
export default {
  name: 'Tag',
  props: {
    content: {
      type: String,
      required: true,
    },
  },
}
</script>

<template>
  <span class="tag">
    <span class="content">{{ content }}</span>
    <span class="close">&#10005;</span>
  </span>
</template>

<style scoped>
.tag {
  padding: 8px;
  cursor: default;
  margin-right: 8px;
  border: 1px solid transparent;
  border-radius: 4px;
}

.tag .content {
  font-size: 14px;
  margin-right: 6px;
}

.tag .close {
  font-size: 12px;
  cursor: pointer;
}
</style>

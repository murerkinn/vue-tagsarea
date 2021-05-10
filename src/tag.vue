<script>
export default {
  name: 'Tag',
  props: {
    content: {
      type: String,
      required: true,
    },
    theme: {
      type: String,
      required: false,
      default: 'primary',
    },
    exists: {
      type: Boolean,
      default: false,
    }
  }
}
</script>

<template>
  <span class="tag" :class="{ 'danger': exists, [theme]: theme }">
    <!-- eslint-disable -->
    <span class="content">{{ content }}</span>
    <span class="close" @click="$emit('remove')">&#10005;</span>
  </span>
</template>

<style scoped>
.tag {
  padding: 0 7px;
  cursor: default;
  margin: 0 4px 4px 0;
  border: 1px solid transparent;
  border-radius: 4px;
}

.tag .content {
  font-size: 12px;
  line-height: 20px;
  margin-right: 4px;
  vertical-align: middle;
}

.tag .close {
  font-size: 12px;
  cursor: pointer;
  vertical-align: middle;
}

.tag.primary {
  background-color: #cfe2ff;
  color: #084298;
  border-color: #b6d4fe;
}

.tag.secondary {
  background-color: #e2e3e5;
  color: #41464b;
  border-color: #d3d6d8;
}

.tag.success {
  background-color: #d1e7dd;
  color: #0f5132;
  border-color: #badbcc;
}

.tag.danger {
  background-color: #f8d7da !important;
  color: #842029 !important;
  border-color: #f5c2c7 !important;
}

.tag.warning {
  background-color: #fff3cd;
  color: #664d03;
  border-color: #ffecb5;
}

.tag.info {
  background-color: #cff4fc;
  color: #055160;
  border-color: #b6effb;
}

.tag.light {
  background-color: #fefefe;
  color: #636464;
  border-color: #fdfdfe;
}

.tag.dark {
  background-color: #d3d3d4;
  color: #141619;
  border-color: #bcbebf;
}
</style>

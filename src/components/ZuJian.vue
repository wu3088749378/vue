<template>
  <div class="container" :style="{ height: containerHeight }">
    <div class="content" ref="content">
      <slot></slot>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      containerHeight: 'auto'
    };
  },
  mounted() {
    this.updateContainerHeight();
    window.addEventListener('resize', this.updateContainerHeight);
  },
  destroyed() {
    window.removeEventListener('resize', this.updateContainerHeight);
  },
  methods: {
    updateContainerHeight() {
      const contentHeight = this.$refs.content.offsetHeight;
      const maxHeight = window.innerHeight * 0.8;
      this.containerHeight = Math.min(contentHeight, maxHeight) + 'px';
    }
  }
};
</script>

<style>
.container {
  width: 80%; /* 固定宽度为80% */
  max-width: 600px; /* 最大宽度 */
  margin: 0 auto; /* 居中 */
  background-color: #f0f0f0; /* 浅灰色背景 */
  overflow: hidden; /* 防止内容溢出 */
}

.content {
  display: flex;
  justify-content: center;
  align-items: center;
  transition: height 0.3s ease; /* 平滑过渡效果 */
}
</style>

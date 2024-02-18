<template>
  <div class="card">
    <h3>{{ user.name }}</h3>
    <p>Email: {{ user.email }}</p>
    <p>Role: {{ user.role }}</p>
    <button @click="updateUser">Update</button>
  </div>
</template>

<script>
export default {
  props: {
    user: {
      type: Object,
      required: true
    }
  },
  methods: {
    updateUser() {
      // 当用户点击更新按钮时，调用更新用户的 API，并在成功更新后触发更新事件
      // 假设后端更新 API 的路径为 '/api/updateUser'
      // 假设更新 API 需要用户的 ID，假设 user 对象中有 id 字段
      // 假设更新成功后后端返回了新的用户列表数据
      axios.post('/api/updateUser', { userId: this.user.id })
        .then(response => {
          // 更新成功后触发更新事件
          this.$emit('update');
        })
        .catch(error => {
          console.error('更新用户失败', error);
        });
    }
  }
};
</script>

<style scoped>
.card {
  border: 1px solid #ccc;
  padding: 10px;
  margin-bottom: 10px;
}
</style>

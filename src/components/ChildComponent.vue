<template>
  <div>
    <div v-for="user in users" :key="user.id">
      <CardComponent :user="user" @update="updateUser" />
    </div>
  </div>
</template>

<script>
import CardComponent from './CardComponent.vue';

export default {
  components: {
    CardComponent
  },
  props: {
    users: {
      type: Array,
      required: true
    }
  },
  methods: {
    updateUser() {
      // 当用户点击更新按钮时，触发更新用户列表事件
      this.$emit('updateUserList');
    }
  }
};
</script>

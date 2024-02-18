<template>
  <div>
    <ChildComponent :users="users" @updateUserList="updateUserList" />
  </div>
</template>

<script>
import axios from 'axios';
import ChildComponent from './ChildComponent.vue';

export default {
  components: {
    ChildComponent
  },
  data() {
    return {
      users: []
    };
  },
  mounted() {
    this.fetchUserList();
  },
  methods: {
    fetchUserList() {
      axios.get('/api/users')
        .then(response => {
          this.users = response.data;
        })
        .catch(error => {
          console.error('获取用户列表错误', error);
        });
    },
    updateUserList() {
      // 当用户点击更新按钮时，重新获取用户列表数据
      this.fetchUserList();
    }
  }
};
</script>

<template>
  <div>
    <el-table :data="userData" :default-sort="{prop: 'registrationDate', order: 'descending'}">
      <el-table-column label="Username" prop="username"></el-table-column>
      <el-table-column label="Email" prop="email"></el-table-column>
      <el-table-column label="Registration Date" prop="registrationDate" sortable :formatter="formatDate"></el-table-column>
      <el-table-column label="Status" prop="status.description"></el-table-column>
      <el-table-column label="Actions">
        <template slot-scope="scope">
          <el-button @click="editUser(scope.row)" type="primary" size="mini">编辑</el-button>
          <el-button @click="toggleUserStatus(scope.row)" :type="scope.row.status.code === 1 ? 'danger' : 'success'" size="mini">
            {{ scope.row.status.code === 1 ? 'Disable' : 'Enable' }}
          </el-button>
          <el-button @click="confirmDeleteUser(scope.row)" type="danger" size="mini">Delete</el-button>
        </template>
      </el-table-column>
    </el-table>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      userData: []
    };
  },
  created() {
    this.fetchUserData();
  },
  methods: {
    fetchUserData() {
      axios.get('/api/users')
        .then(response => {
          this.userData = response.data.map(user => {
            return {
              ...user,
              registrationDate: new Date(user.registrationDate)
            };
          });
        })
        .catch(error => {
          console.error('获取用户数据错误', error);
        });
    },
    formatDate(date) {
      return new Date(date).toLocaleDateString();
    },
    toggleUserStatus(user) {
      const newStatus = user.status.code === 1 ? 0 : 1;
      axios.post(`/api/users/${user._id}/status`, { status: newStatus })
        .then(() => {
          user.status.code = newStatus;
          user.status.description = newStatus === 1 ? 'Active' : 'Inactive';
        })
        .catch(error => {
          console.error('切换用户状态错误', error);
        });
    },
    editUser(user) {
      // 实现编辑用户的逻辑
    },
    confirmDeleteUser(user) {
      this.$confirm('你确定要删除这个用户吗？', 'Warning', {
        confirmButtonText: '确认',
        cancelButtonText: '取消',
        type: 'warning'
      }).then(() => {
        this.deleteUser(user);
      }).catch(() => {
        this.$message({
          type: 'info',
          message: '取消删除'
        });
      });
    },
    deleteUser(user) {
      axios.delete(`/api/users/${user._id}`)
        .then(() => {
          this.userData = this.userData.filter(u => u._id !== user._id);
          this.$message({
            type: 'success',
            message: '删除用户成功'
          });
        })
        .catch(error => {
          console.error('删除用户失败: ', error);
        });
    }
  }
};
</script>

<template>
  <div>
    <el-table :data="groupList" style="width: 100%" :default-sort="{ prop: 'groupId', order: 'ascending' }"
      :row-class-name="rowClassName" :pagination="pagination" :sort-method="sortMethod" :filter-method="filterMethod">
      <el-table-column label="Group ID" prop="groupId"></el-table-column>
      <el-table-column label="Group Name" prop="groupName"></el-table-column>
      <el-table-column label="Users">
        <template slot-scope="scope">
          <el-table :data="scope.row.users" style="width: 100%" :default-sort="{ prop: 'id', order: 'ascending' }">
            <el-table-column label="User ID" prop="id"></el-table-column>
            <el-table-column label="Name" prop="name"></el-table-column>
            <el-table-column label="Email" prop="email"></el-table-column>
            <el-table-column label="Role" prop="role"></el-table-column>
            <el-table-column label="CreatedAt">
              <template slot-scope="userScope">
                {{ formatDate(userScope.row.createdAt) }}
              </template>
            </el-table-column>
          </el-table>
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
      groupList: [],
      pagination: {
        currentPage: 1,
        pageSize: 10
      }
    };
  },
  created() {
    this.fetchData();
  },
  methods: {
    async fetchData() {
      try {
        const response = await axios.get('API');
        this.groupList = response.data.data;
      } catch (error) {
        console.error('Error:', error);
      }
    },
    formatDate(dateString) {
      const date = new Date(dateString);
      return date.toLocaleDateString();
    },
    rowClassName() {
      return 'nested-table-row';
    },
    sortMethod(a, b) {
      // 自定义排序方法
      return a.groupId - b.groupId;
    },
    filterMethod(value, row) {
      // 自定义筛选方法
      return row.groupName.toLowerCase().includes(value.toLowerCase());
    }
  }
};
</script>

<style scoped>
.nested-table-row {
  background-color: #f5f5f5;
}
</style>

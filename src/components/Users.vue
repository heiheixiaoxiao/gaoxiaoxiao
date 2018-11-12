<template>
  <div class="users">
    <el-breadcrumb separator-class="el-icon-arrow-right">
      <el-breadcrumb-item :to="{ path: '/users' }" >用户管理</el-breadcrumb-item>
      <el-breadcrumb-item>用户列表</el-breadcrumb-item>
    <div style="margin-top: 30px;" class="search">
      <el-input placeholder="请输入内容" v-model="query" class="input-with-select">
        <el-button slot="append" icon="el-icon-search" @click="search"></el-button>
      </el-input>
      <el-button type="success" plain>用户添加</el-button>
    </div>
    </el-breadcrumb>
    <el-table :data="userList"  style="width: 100%">
      <el-table-column prop="username" label="姓名"  width="180">
      </el-table-column>
      <el-table-column prop="email" label="邮箱" width="180">
      </el-table-column>
      <el-table-column prop="mobile" label="电话" width="180">
      </el-table-column>
    <el-table-column label="状态" width="180">
      <template slot-scope="scope">
        {{scope.row.mg_status}}
        <el-switch v-model="scope.row.mg_state" active-color="#13ce66" inactive-color="#ff4949">
      </el-switch>
       </template>
    </el-table-column>
    <el-table-column label="操作">
  <template slot-scope="scope">
    <el-button size="small" type="primary" plain  icon="el-icon-edit" ></el-button>
    <el-button size="small" type="danger" plain icon="el-icon-delete" @click="delUser(scope.row.id)"></el-button>
    <el-button size="small" type="success" plain icon="el-icon-check" >分配角色</el-button>
  </template>
    </el-table-column>
  </el-table>
  <!-- <el-pagination background layout="prev, pager, next" :total="1000"> -->

<!-- </el-pagination> -->
<template>
  <div class="block">
    <el-pagination
      @size-change="handleSizeChange"
      @current-change="handleCurrentChange"
      :current-page="currentPage4"
      :page-sizes="[2,4,6,8]"
      :page-size="pageSize"
      layout="total, sizes, prev, pager, next, jumper"
      :total="total"
      background>
    </el-pagination>
  </div>
</template>
  </div>
</template>
<script>
import axios from 'axios'
export default {
  data() {
    return {
      id: '',
      query: '',
      currentPage: 1,
      pageSize: 2,
      userList: [],
      total: 0,
      currentPage4: 4
    }
  },
  methods: {
    getUserList() {
      axios({
        url: 'http://localhost:8888/api/private/v1/users',
        method: 'get',
        params: {
          query: this.query,
          pagenum: this.currentPage,
          pagesize: this.pageSize
        },
        headers: {
          Authorization: localStorage.getItem('token')
        }
      }).then(res => {
        console.log(res.data)
        if (res.data.meta.status === 200) {
          this.userList = res.data.data.users
          this.total = res.data.data.total
        }
      })
    },
    handleSizeChange(val) {
      this.pageSize = val
      this.getUserList()
    },
    handleCurrentChange(val) {
      this.currentPage = val
      this.getUserList()
    },
    search() {
      this.getUserList()
    },
    delUser(id) {
      console.log(id)
      this.$confirm('你确定要删除这个用户吗?', '温馨提示', {
        confirmButtonText: '确定',
        cancelButtonText: '取消',
        type: 'warning'
      })
        .then(() => {
          axios({
            url: `http://localhost:8888/api/private/v1/users/${id}`,
            method: 'delete',
            headers: {
              Authorization: localStorage.getItem('token')
            }
          }).then(res => {
            if (res.data.meta.status === 200) {
              if (this.userList.length === 1 && this.currentPage > 1) {
                this.currentPage--
              }
              this.getUserList()
            }
          })
          this.$message({
            type: 'success',
            message: '删除成功!'
          })
        })
        .catch(() => {
          this.$message({
            type: 'info',
            message: '已取消删除'
          })
        })
    }
  },
  created() {
    this.getUserList()
  }
}
</script>

<style>
.search {
  display: flex;
  justify-content: flex-start;
  width: 500px;
}
.el-table {
  margin-top: 10px;
}
.block {
  text-align: left;
}
</style>

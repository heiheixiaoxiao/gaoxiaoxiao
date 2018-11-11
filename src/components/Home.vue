<template>
  <el-container class="home">
    <!-- 头部区域 -->
    <el-header>
      <div class="logo"></div>
      <h1>电商后台管理系统</h1>
      <div class="right">
      <span>欢迎光临</span>
      <a href="#" @click.prevent="close">退出</a>
      </div>
    </el-header>
    <!-- 侧边栏导航区 -->
    <el-container>
      <el-aside width="200px">
        <el-menu
      default-active="2"
      class="el-menu-vertical-demo"
      @open="handleOpen"
      @close="handleClose"
      background-color="#545c64"
      text-color="#fff"
      active-text-color="#ffd04b"
      unique-opened>
      <el-submenu index="1">
        <template slot="title">
          <i class="el-icon-location"></i>
          <span>用户管理</span>
        </template>
          <el-menu-item index="1-1">
          <i class="el-icon-menu"></i>
          <span slot="title">用户列表</span>
          </el-menu-item>
      </el-submenu>
       <el-submenu index="2">
        <template slot="title">
          <i class="el-icon-location"></i>
          <span>权限管理</span>
        </template>
          <el-menu-item index="2-1">
            <i class="el-icon-menu"></i>
            <span slot="title">角色列表</span>
          </el-menu-item>
       <el-menu-item index="2-2">
            <i class="el-icon-menu"></i>
            <span slot="title">权限列表</span>
       </el-menu-item>
      </el-submenu>
    </el-menu>
      </el-aside>
      <el-main>
        <!-- 内容展示区 -->
        <el-breadcrumb separator-class="el-icon-arrow-right">
        <el-breadcrumb-item :to="{ path: '/' }">用户管理</el-breadcrumb-item>
        <el-breadcrumb-item>用户列表</el-breadcrumb-item>
      </el-breadcrumb>
        <div style="margin-top: 15px;" class="search">
          <el-input placeholder="请输入关键字" v-model="input5" class="input-with-select">
            <el-button slot="append" icon="el-icon-search"></el-button>
          </el-input>
           <el-button type="success" style="margin-left: 10px;" plain>用户添加</el-button>
      </div>
       <template>
    <el-table
      :data="tableData"
      style="width: 100%">
      <el-table-column
        prop="date"
        label="姓名"
        width="180">
      </el-table-column>
      <el-table-column
        prop="name"
        label="邮箱"
        width="180">
      </el-table-column>
      <el-table-column
        prop="address"
        label="电话">
      </el-table-column>
      <el-table-column
        prop="address"
        label="状态">
      </el-table-column>
      <el-table-column
        prop="address"
        label="操作">
      </el-table-column>
    </el-table>
  </template>
      </el-main>
    </el-container>
  </el-container>
</template>

<script>
export default {
  data() {
    return {
      input5: '',
      tableData: [
        {
          date: '2016-05-02',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        }
      ]
    }
  },
  // 二级导航展开和关闭操作
  methods: {
    handleOpen(key, keyPath) {
      console.log(key, keyPath)
    },
    handleClose(key, keyPath) {
      console.log(key, keyPath)
    },
    // 退出系统操作
    close() {
      this.$confirm('你确定要退出系统吗?', '温馨提示', {
        confirmButtonText: '确定',
        cancelButtonText: '取消',
        type: 'warning'
      })
        .then(() => {
          localStorage.removeItem('token')
          this.$router.push('/login')
          this.$message.success('成功退出系统')
        })
        .catch(() => {
          this.$message.info('取消了退出操作')
        })
    }
  }
}
</script>

<style lang="less" scope>
.home {
  height: 100%;
  // 头部区域
  .el-header {
    background-color: #b3c1cd;
    position: relative;
    .logo {
      height: 60px;
      width: 180px;
      background: url('../assets/logo.png') no-repeat center center;
      background-size: contain;
      position: absolute;
      left: 20px;
      top: 50%;
      transform: translateY(-50%);
    }
    .right {
      width: 180px;
      height: 60px;
      position: absolute;
      right: 20px;
      top: 50%;
      transform: translateY(-50%);
      line-height: 60px;
      text-align: right;
      font-size: 18px;
      font-weight: 700;
      a {
        color: darkorange;
      }
    }
    h1 {
      line-height: 60px;
      text-align: center;
      font-size: 30px;
    }
  }
  // 侧边栏导航区域
  .el-aside {
    background-color: #545c64;
    text-align: center;
  }
  // 内容展示区域
  .el-main {
    background-color: #d4dfe4;
    margin-bottom: 20px;
    .search {
      display: flex;
      justify-content: flex-start;
      width: 500px;
    }
    .el-table {
      margin-top: 10px;
    }
  }
}
</style>

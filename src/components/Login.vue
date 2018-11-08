<template>
<div class="login">
<el-form ref="form" :model="form" label-width="80px">
  <img src="../assets/1.jpg" alt="">
   <el-form-item label="用户名">
    <el-input v-model="form.username"></el-input>
  </el-form-item>
  <el-form-item label="密码">
    <el-input v-model="form.password" type="password"></el-input>
  </el-form-item>
    <el-button type="primary">登录</el-button>
    <el-button>重置</el-button>
</el-form>
</div>
</template>
<script>
export default {
  data() {
    return {
      form: {
        username: '',
        password: ''
      }
    }
  }
}
</script>
<style lang="less">
.login {
  background-color: #2d434c;
  height: 100%;
  overflow: hidden;
  .el-form {
    width: 400px;
    margin: 200px auto;
    background-color: #fff;
    padding: 75px 40px 15px;
    border-radius: 20px;
    position: relative;
  }
  img {
    width: 130px;
    height: 130px;
    border-radius: 50%;
    border: 10px solid #fff;
    position: absolute;
    left: 50%;
    top: -35%;
    transform: translateX(-50%);
  }
  button {
    margin-left: 30px;
  }
  button:nth-child(2) {
    margin-left: 40px;
  }
}
</style>

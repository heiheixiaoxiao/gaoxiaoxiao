<template>
<div class="login">
<el-form ref="form" :rules="rules" status-icon :model="form" label-width="80px" >
  <img src="../assets/1.jpg" alt="">
   <el-form-item label="用户名" prop="username" ref="username">
    <el-input v-model="form.username"></el-input>
  </el-form-item>
  <el-form-item label="密码" prop="password">
    <el-input v-model="form.password" type="password" ref="password" @keyup.enter.native="login" ></el-input>
  </el-form-item>
    <el-button type="primary" @click="login">登录</el-button>
    <el-button  @click="reset">重置</el-button>
</el-form>
</div>
</template>
<script>
import axios from 'axios'
export default {
  data() {
    return {
      form: {
        username: '',
        password: ''
      },
      rules: {
        username: [
          { required: true, message: '用户名不能为空', trigger: 'change' },
          { min: 3, max: 6, message: '长度在 3 到 6 个字符', trigger: 'change' }
        ],
        password: [
          { required: true, message: '密码不能为空', trigger: 'change' },
          {
            min: 6,
            max: 12,
            message: '长度在 6 到 12 个字符',
            trigger: 'change'
          }
        ]
      }
    }
  },
  methods: {
    reset() {
      this.$refs.form.resetFields()
    },
    login() {
      this.$refs.form.validate(valid => {
        if (valid) {
          axios({
            url: 'http://localhost:8888/api/private/v1/login',
            method: 'post',
            data: this.form
          }).then(res => {
            if (res.data.meta.status === 200) {
              this.$message.success('登录成功')
              localStorage.setItem('token', res.data.data.token)
              this.$router.push('./Home.vue')
            } else {
              this.$message.error('登录失败')
            }
          })
        }
      })
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

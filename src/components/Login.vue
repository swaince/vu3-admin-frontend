<template>
<div class="login-container">
  <div class="login-panel">
    <div class="logo-wrapper">
      <img src="@/assets/vue.svg" alt="logo"/>
    </div>
    <el-form
      :model="loginForm"
      class="login-form"
      ref="loginFormRef"
      :rules="rules"
    >
      <el-form-item label="账户" prop="username">
        <el-input v-model="loginForm.username" :prefix-icon="User"></el-input>
      </el-form-item>
      <el-form-item label="密码" prop="password">
        <el-input type="password" v-model="loginForm.password" :prefix-icon="Lock"></el-input>
      </el-form-item>
      <el-form-item class="btns">
        <el-button type="primary" @click="submitForm(loginFormRef)">登录</el-button>
        <el-button type="info" @click="resetForm(loginFormRef)">取消</el-button>
      </el-form-item>
    </el-form>
  </div>
</div>
</template>

<script setup lang="ts">
import {reactive, ref} from "vue";
import {FormInstance, FormRules} from "element-plus";
import {User, Lock} from '@element-plus/icons-vue'

interface LoginForm {
  username: '',
  password: ''
}

const loginForm = reactive<LoginForm>({
  username: '',
  password: ''
})

const loginFormRef = ref<FormInstance>()

const rules = reactive<FormRules<LoginForm>>({
  username: [
    {
      trigger: 'blur',
      required: true,
      message: "账户不能为空"
    },
    {
      max: 20,
      min: 5,
      message: "账户长度必须在5 - 20之间",
      trigger: 'blur'
    }
  ],
  password: [
    {
      trigger: 'blur',
      required: true,
      message: "密码不能为空"
    },
    {
      max: 15,
      min: 6,
      message: "密码长度必须在6 - 15之间",
      trigger: 'blur'
    }
  ]
})

  const submitForm = async (formData: FormInstance | undefined) => {
    if (!formData) {
      return
    }

    await formData.validate((valid, fields) => {
      if (valid) {
        console.log("submit")
      } else {
        console.log("validate error", fields)
      }
    })
  }

  const resetForm = (formData: FormInstance | undefined) => {
    if (!formData) {
      return
    }

    formData.resetFields()
  }
</script>

<style scoped lang="scss">
.login-container {
  width: 100vw;
  height: 100vh;
  background-color: #2376b7;
  display: flex;
  justify-content: center;
  align-items: center;

  .login-panel {
    width: 450px;
    height: 300px;
    background-color: #fff;
    border-radius: 10px;
    position: relative;

    .logo-wrapper {
      width: 130px;
      height: 130px;
      border-radius: 50%;
      border: 1px solid #ccc;
      padding: 10px;
      box-shadow: 0 0 10px #ddd;
      background-color: #fff;
      position: absolute;
      left: calc(50% - 65px);
      top: -50px;

      img {
        width: 100%;
        height: 100%;
        border-radius: 50%;
        background-color: #eee;
      }
    }

    .login-form {
      position: absolute;
      bottom: 0;
      width: 100%;
      padding: 20px;
    }
  }
}
</style>

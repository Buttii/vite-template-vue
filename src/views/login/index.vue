<template>
  <el-form :model="userInfo" :rules="rules" ref="form">
    <el-form-item prop="username">
      <el-input
        v-model="userInfo.username"
        prefix-icon="el-icon-user"
        placeholder="请输入密码"
        size="small"
      ></el-input>
    </el-form-item>
    <el-form-item prop="password">
      <el-input
        type="password"
        v-model="userInfo.password"
        prefix-icon="el-icon-lock"
        show-password
        placeholder="请输入密码"
        size="small"
      ></el-input>
    </el-form-item>
    <el-form-item>
      <el-button type="primary" @click="handleClick" size="small">登 录</el-button>
    </el-form-item>
  </el-form>
</template>

<script setup>
import { ElForm, ElFormItem, ElInput, ElButton } from "element-plus";
import { reactive, ref } from "vue";
import {useRouter} from "vue-router"

// router实例
const router = useRouter()
// 用户信息
const userInfo = reactive({
  username: "",
  password: "",
});
// 获取el-form实例
const form = ref(null)
// userInfo校验规则
const rules = {username: {required: true, message: "请输入用户名"}, password: {required: true, message: "请输入密码"}}
// 点击登录
function handleClick() {
  form.value.validate(valid => {
    if(valid) {
      router.push("/")
    }
    else console.log("请正确填写信息！");
  })
}

</script>
<style lang="less" scoped>
.el-form {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  box-shadow: 0 0 6px 2px rgba(0, 0, 0, .1);
  padding: 22px 22px 0;
  border-radius: 2px;
  .el-input, .el-button {
    width: 320px;
  }
}
</style>
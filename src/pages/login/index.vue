<template>
  <h1>用户登录</h1>
  <van-form @submit="onSubmit">
    <van-cell-group inset>
      <van-field v-model="from.userName" name="用户名" label="用户名" placeholder="用户名" :rules="[{ required: true, message: '请填写用户名' }]" />
      <van-field v-model="from.passWord" type="password" name="密码" label="密码" placeholder="密码" :rules="[{ required: true, message: '请填写密码' }]" />
    </van-cell-group>
    <div style="margin: 16px">
      <van-button round block type="primary" native-type="submit"> 登录 </van-button>
    </div>
  </van-form>
</template>

<script setup>
import { reactive, getCurrentInstance } from 'vue'
import { useRouter } from 'vue-router'
// 获取当前vue实例
const { proxy } = getCurrentInstance()
const router = useRouter()
const from = reactive({
  userName: '13086683537',
  passWord: '123456'
})
const onSubmit = async () => {
  let res = await proxy.$api.login(from)
  // console.log(res)
  if (res) {
    localStorage.setItem('token', res.token)
    localStorage.setItem('userInfo', JSON.stringify(res.userInfo))
    router.push('/home')
  }
}
</script>

<style lang="less" scoped>
h1 {
  text-align: center;
}
</style>

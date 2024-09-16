<script setup lang="ts">
import { ref } from 'vue'

const email = ref('')
const password = ref('')
const loading = ref(false)
const errorMessage = ref('')
const { $supabase } = useNuxtApp()

async function handleLogin() {
  loading.value = true
  errorMessage.value = ''

  try {
    const { error } = await $supabase.client.auth.signInWithPassword({
      email: email.value,
      password: password.value,
    })

    if (error)
      throw error

    // 登录成功,重定向到首页
    navigateTo('/')
  }
  catch (error: any) {
    errorMessage.value = error.message
  }
  finally {
    loading.value = false
  }
}
</script>

<template>
  <div class="login-container">
    <van-form @submit="handleLogin">
      <van-cell-group inset>
        <van-field
          v-model="email"
          name="email"
          label="邮箱"
          placeholder="请输入邮箱"
          :rules="[{ required: true, message: '请填写邮箱' }]"
        />
        <van-field
          v-model="password"
          type="password"
          name="password"
          label="密码"
          placeholder="请输入密码"
          :rules="[{ required: true, message: '请填写密码' }]"
        />
      </van-cell-group>
      <div style="margin: 16px;">
        <van-button round block type="primary" native-type="submit" :loading="loading">
          登录
        </van-button>
      </div>
    </van-form>
    <van-notice-bar v-if="errorMessage" type="danger">
      {{ errorMessage }}
    </van-notice-bar>
  </div>
</template>

<style scoped>
.login-container {
  padding: 20px;
  max-width: 400px;
  margin: 0 auto;
}
</style>

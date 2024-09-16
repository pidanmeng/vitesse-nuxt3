<script setup lang="ts">
definePageMeta({
  layout: 'fullscreen',
})

const { $trpcClient } = useNuxtApp()
const { data } = await $trpcClient.hello.useQuery({ text: 'tRPC' })

const router = useRouter()
function login() {
  router.push('/login')
}
</script>

<template>
  <div flex="~ col" justify="center" items="center">
    <p>{{ data?.greeting }}</p>
    <van-button type="primary" @click="login">
      登录
    </van-button>
  </div>
</template>

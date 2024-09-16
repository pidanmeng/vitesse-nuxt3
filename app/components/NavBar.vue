<script setup lang="ts">
const user = useSupabaseUser()
const { $supabase } = useNuxtApp()

const username = computed(() => user.value?.email?.split('@')[0] || '用户')

async function handleLogout() {
  await $supabase.client.auth.signOut()
  navigateTo('/login')
}
</script>

<template>
  <van-nav-bar
    :title="`欢迎, ${username}`"
    left-text="返回"
    right-text="登出"
    left-arrow
    @click-left="$router.back()"
    @click-right="handleLogout"
  />
</template>

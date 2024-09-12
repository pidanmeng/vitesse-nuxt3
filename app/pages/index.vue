<script setup lang="ts">
import { appName } from '~/constants'

const { $trpcClient } = useNuxtApp()
const { data } = await $trpcClient.hello.useQuery({ text: 'tRPC' })
</script>

<template>
  <div>
    <p>{{ data?.greeting }}</p>
  </div>
</template>

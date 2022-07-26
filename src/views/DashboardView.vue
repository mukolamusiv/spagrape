<template>
  <main>
    <div class="wrap-content">
      тут буде текст
    </div>
  </main>
</template>

<script setup>
import { useStore } from '@/store'
const { store } = useStore()
store.ui.primeTitle = 'Дошка'
</script>

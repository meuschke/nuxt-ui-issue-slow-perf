<template>
  <div>
    <h1>10,000 Random Buttons</h1>
    <div v-for="(button, idx) in buttons" :key="button.id" style="margin-bottom: 8px;">
      <UButton @click="showCards(idx)">{{ button.text }}</UButton>
      <div v-if="button.showCards" style="display: flex; gap: 8px; margin-top: 4px;">
        <div v-for="card in button.cards" :key="card.id" style="border: 1px solid #ccc; padding: 8px; border-radius: 4px; background: #f9f9f9;">
          {{ card.text }}
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

function randomText(length = 8) {
  const chars = 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789'
  let result = ''
  for (let i = 0; i < length; i++) {
    result += chars.charAt(Math.floor(Math.random() * chars.length))
  }
  return result
}

const buttons = ref(Array.from({ length: 10000 }, (_, i) => ({
  id: i,
  text: randomText(10),
  showCards: false,
  cards: [] as { id: number, text: string }[],
})))

function showCards(idx: number) {
  const btn = buttons.value[idx]
  if (!btn.showCards) {
    btn.cards = Array.from({ length: 3 }, (_, i) => ({
      id: i,
      text: randomText(20),
    }))
    btn.showCards = true
  } else {
    btn.showCards = false
  }
}
</script>

<style scoped>
button {
  padding: 6px 12px;
  border-radius: 4px;
  border: 1px solid #888;
  background: #eee;
  cursor: pointer;
  font-size: 14px;
}
button:hover {
  background: #ddd;
}
</style> 
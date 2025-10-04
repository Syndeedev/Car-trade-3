<template>
  <header class="sticky top-0 z-50 space-x-1 border-b-0 bg-white shadow-md">
    <div class="flex justify-between items-center p-4">
      <NuxtLink class="text-3xl font-mono" to="/">Car trade</NuxtLink>
      <button class="text-white bg-blue-500 px-8 py-2 rounded">Login</button>
    </div>
    <div class="py-2 px-4 bg-blue-500 flex justify-between items-center">
      <client-only>
        <Vue3Marquee>
          <span
            class="px-20 text-2xl"
            v-for="(word, index) in helloArray"
            :key="index"
          >
            {{ word }}
          </span>
        </Vue3Marquee>
      </client-only>
      <!-- <client-only>
        <Marquee :speed="140">
          <span>📈 Apple $178.34</span>
          <span>📉 Tesla $245.18</span>
          <span>💰 Bitcoin $66,540</span>
          <span>🏦 Federal Reserve Update</span>
        </Marquee>
      </client-only> -->
    </div>
  </header>
</template>
<script setup>
const helloArray = [
  "📈 Apple $178.34",
  "📉 Tesla $245.18",
  "💰 Bitcoin $66,540",
  "🏦 Federal Reserve Update",
];
</script>
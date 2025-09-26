<template>
  <div
    class="font-serif w-[700px] my-8 text-md rounded bg-white flex items-center justify-between overflow-hidden drop-shadow-sm mx-auto"
  >
    <SearchIcon class="ml-4" />
    <input
      type="text"
      class="px-2 py-3 w-full text-md rounded focus:outline-none"
      placeholder="Search for stocks..."
      :class="cityError ? 'border-red-500 border' : ''"
      v-model="city"
    />
    <button class="bg-blue-500 p-3 text-white" @click="handleSearch()">
      Search
    </button>
  </div>
</template>
<script setup>
const city = ref("");
const cityError = ref(false);
const handleSearch = () => {
  if (!city.value) {
    return (cityError.value = true);
  }
  navigateTo(`/city/${city.value}/car`);
};
</script>
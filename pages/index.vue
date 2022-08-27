<template>
  <main class="w-screen h-screen grid place-items-center bg-gray-50">
    <div class="text-center">
      <h1 class="text-4xl font-semibold">
        Welcome to
        <span class="text-4xl font-bold text-green-400">Git Stage</span>
      </h1>
      <p>Learn or Review Git <span class="underline">ASAP</span></p>
      <br />
      <div>
        <button
          class="font-semibold shadow-md m-1 px-6 py-2 bg-gray-200 hover:bg-gray-300 rounded-lg"
        >
          <NuxtLink to="/about">About</NuxtLink>
        </button>
        <button
          class="font-semibold shadow-md m-1 px-6 py-2 bg-green-400 hover:bg-green-500 text-gray-50 rounded-lg"
        >
          <NuxtLink to="/learn">Begin →</NuxtLink>
        </button>
      </div>
    </div>
  </main>
</template>

<script lang="ts">
import Vue from "vue";

export default Vue.extend({
  name: "IndexPage",
});
</script>

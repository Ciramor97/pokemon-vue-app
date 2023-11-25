<script setup>
import Home from "./views/Home.vue";
</script>

<template>
  <div class="p-14">
    <router-link
      to="/"
      class="flex justify-center items-center text-4xl text-yellow-700"
      >Pokemon Picker</router-link
    >
    <router-view></router-view>
  </div>
</template>

<style scoped></style>

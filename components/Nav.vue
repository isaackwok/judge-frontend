<template>
  <div class="flex v-bg-green shadow">
    <label class="text-white text-lg mr-10 p-3 truncate">
      NLP Assignment 6
    </label>
    <NuxtLink to="/"
      class="text-white text-lg border-white  p-3 mr-10 hover:border-orange-300 hover:text-orange-300"
      :class="{'border-b-2': $route.name === 'index'}"
      href="#"
    >
      Upload
    </NuxtLink>
    <NuxtLink to="/leaderboard"
      class="text-white text-lg border-white p-3 hover:border-orange-300 hover:text-orange-300"
      :class="{'border-b-2': $route.name === 'leaderboard'}"
      href="#"
    >
      Leaderboard
    </NuxtLink>
  </div>
</template>

<script>
export default {};
</script>
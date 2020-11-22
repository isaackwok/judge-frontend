<template>
  <div class="flex flex-col">
    <Nav />
    <div class="self-center text-center p-3">
      <Nuxt />
    </div>
  </div>
</template>

<style>
body,
html {
  background-color: rgb(241, 237, 237);
}
.v-green {
  color: #42b983;
}
.v-bg-green {
  background-color: #42b983;
}
p {
  margin-top: 2rem;
  margin-bottom: 0.5rem;
}

.required::before {
  content: "*";
  color: red
}
table th {
  color: #42b983;
}

table tbody > tr:last-child {
  border: none
}
</style>

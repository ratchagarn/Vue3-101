<template>
  <div class="container">
    <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/todo">Todo</router-link>
    </div>
    <router-view />
  </div>
</template>

<style scoped>
#nav {
  margin: 20px 0;
}
</style>

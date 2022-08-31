<template>
  <nav>
    <p class="logo">GameBase</p>
    <ul class="nav-links">
      <li class="nav-link"><router-link to="/">Home</router-link></li>
      <li class="nav-link"><router-link to="/games">Games</router-link></li>
      <li class="nav-link"><router-link to="/about">About</router-link></li>
    </ul>

  </nav>
</template>

<script>
export default {
  name: "NavComponent"
}
</script>

<style scoped>
nav {
  padding: 20px;
  background-color: #2c2c54;
  border-bottom: 2px solid #474787;
  display: flex;
  align-items: center;
  justify-content: space-around;
}

.nav-links {
  list-style: none;
  display: flex;
}

.nav-link {
  margin-right: 20px;
}

.nav-link a {
  text-decoration: none;
  font-weight: bold;
  color: #fff;
}

.nav-link a:hover {
  color: #B33771;
}

.nav-link a.router-link-exact-active {
  color: #B33771;
}

.logo {
  font-weight: bold;
}
</style>
<template>
  <nav-component></nav-component>
  <div class="container">
    <router-view/>
  </div>

</template>

<script>
  import NavComponent from "@/components/NavComponent";
  export default {
    components: {
      NavComponent
    }
  }
</script>
<style>
body {
  background-color: #3B3B98;
  margin: 0;
  padding: 0;
}

.container {
  max-width: 1300px;
  margin-left: auto;
  margin-right: auto;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #fff;
}
</style>
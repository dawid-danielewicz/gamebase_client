<template>
  <div class="page-header">
    <h1>Games</h1>
    <div class="icon-wrapper">
      <router-link to="/games/create">
        <svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="0 0 512 512" class="icon">
          <path d="M448 256c0-106-86-192-192-192S64 150 64 256s86 192 192 192s192-86 192-192z" fill="none" stroke="currentColor" stroke-miterlimit="10" stroke-width="32"></path>
          <path fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="32" d="M256 176v160"></path>
          <path fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="32" d="M336 256H176"></path>
        </svg>
      </router-link>
    </div>
  </div>
  <div class="lds-ripple" v-if="$apollo.queries.games.loading"><div></div><div></div></div>
  <div class="grid" v-else>
    <div v-for="game in games" :key="game.id" class="card">
      <h2>{{ game.name }}</h2>
      <p>{{ game.description }}</p>
      <p>PEGI: {{ game.age }}</p>
      <p>Relaease Date: {{ game.year }}</p>
    </div>
  </div>
</template>

<script>
import gql from 'graphql-tag';

export default {
  name: "GamesView",
  apollo: {
    games: gql`
        query {
            games {
              id
              name
              description
              age
              year
            }
        }
    `
  }
}
</script>

<style scoped>
.grid {
  display: grid;
  grid-template-columns: auto auto auto;
}

.card {
  background-color: #2c2c54;
  margin: 10px;
  padding: 20px;
  border-radius: 5px;
}

.page-header {
  margin: 50px 0;
  display: flex;
  justify-content: center;
  align-items: center;
}

.icon {
  width: 30px;
  height: 30px;
  color: #B33771;
  display: block;
  margin-left: 10px;
}

.page-header h1 {
  display: inline-block;
}

.icon-wrapper {
  display: flex;
  align-items: center;
  height: 100%;
}

.lds-ripple {
  display: inline-block;
  position: relative;
  width: 80px;
  height: 80px;
}
.lds-ripple div {
  position: absolute;
  border: 4px solid #fff;
  opacity: 1;
  border-radius: 50%;
  animation: lds-ripple 1s cubic-bezier(0, 0.2, 0.8, 1) infinite;
}
.lds-ripple div:nth-child(2) {
  animation-delay: -0.5s;
}
@keyframes lds-ripple {
  0% {
    top: 36px;
    left: 36px;
    width: 0;
    height: 0;
    opacity: 0;
  }
  4.9% {
    top: 36px;
    left: 36px;
    width: 0;
    height: 0;
    opacity: 0;
  }
  5% {
    top: 36px;
    left: 36px;
    width: 0;
    height: 0;
    opacity: 1;
  }
  100% {
    top: 0px;
    left: 0px;
    width: 72px;
    height: 72px;
    opacity: 0;
  }
}

</style>
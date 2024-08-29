<!--https://dev.to/easykiel15/creating-tictactoe-in-vuejs-p15-->

<template>
  <h1 class="text-xl mb-4">Naughts and Crosses</h1>
  <br><br><br><br>
  <div class="flex flex-col items-center mb-8">
    <div v-for="(row, x) in board" :key="x" class="flex">
      <div 
        v-for="(cell, y) in row" 
        :key="y" 
        @click="MakeMove(x, y)" 
        :class="`border border-white w-24 h-24 hover:bg-blue-700 flex items-center justify-center material-icons-outlined text-4xl cursor-pointer ${cell === 'X' ? 'text-pink-500' : 'text-blue-400'}`">
        {{ cell === 'X' ? 'X' : cell === 'O' ? 'O' : '' }}
      </div>
    </div>
  </div>

  <h3 class="text-xl mb-4">---Player {{ player }}'s turn</h3>
  <button @click="ResetGame" class="px-4 py-2 bg-red-500 rounded uppercase font-bold hover:bg-red-600 duration-300">Reset</button>
  <h2 v-if="winner" class="text-6xl font-bold mb-8">Player '{{ winner }}' wins! </h2>
  
</template>

<script>
import { ref, computed } from 'vue';

export default {
  setup() {
    const player = ref('X');
    const board = ref([
      ['', '', ''],
      ['', '', ''],
      ['', '', '']
    ]);

    const calculateWinner = (squares) => {
      const lines = [
        [0,1,2],
        [3,4,5],
        [6,7,8],
        [0,3,6],
        [1,4,7],
        [2,5,8],
        [0,4,8],
        [2,4,6],
      ];
      for (let i = 0; i < lines.length; i++) {
        const [a,b,c] = lines[i];
        if (squares[a] && squares[a] === squares[b] && squares[a] === squares[c]) {
          return squares[a];
        }
      }
      return null;
    };

    const winner = computed(() => calculateWinner(board.value.flat()));

    const MakeMove = (x, y) => {
      if (winner.value) return;
      if (board.value[x][y] !== '') return;
      board.value[x][y] = player.value;
      player.value = player.value === 'X' ? 'O' : 'X';
    };

    const ResetGame = () => {
      board.value = [
        ['', '', ''],
        ['', '', ''],
        ['', '', '']
      ];
      player.value = 'X';
    };

    return {
      player,
      board,
      winner,
      MakeMove,
      ResetGame
    };
  }
};
</script>
















<!-- <script setup>
import { RouterLink, RouterView } from 'vue-router'
//import HelloWorld from './components/HelloWorld.vue'
</script> -->

<!--code guide https://www.blog.duomly.com/vue-js-tutorial-how-to-create-vue-js-app-in-5-minutes/#3-start-a-project-->

<!-- <template>
  <div class="container"><h1>Vue Users</h1></div><br><br><br>
  <div class="container">
    <h3> User credentials below:</h3>
    <table class="table">
      <thead>
        <tr>
          <th scope="col">Id</th>
          <th scope="col">Name</th>
          <th scope="col">Email</th>
          <th scope="col">City</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="user in users" v-bind:key="user.id">
          <th scope="row">{{user.id}}</th>
          <td>{{user.name}}</td>
          <td>{{user.email}}</td>
          <td>{{user.address.city}}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import Users from './components/Users.vue'
import axios from 'axios';

export default {
    name: 'Users',
    data() {
      return {
        users: null,
      };
    },
    created: function() {
      axios
        .get('https://jsonplaceholder.typicode.com/users')
        .then(res => {
          this.users = res.data;
        })
    }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  background-color: aliceblue;
}
</style> -->



<!--old code below-->
<!-- <template>
  <header>
    <img alt="Vue logo" class="logo" src="@/assets/logo.svg" width="125" height="125" />

    <div class="wrapper">
      <HelloWorld msg="You did it! Yay!" />

      <nav>
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/about">About</RouterLink>
      </nav>
    </div>
  </header>

  <RouterView />
</template> 

<style scoped>
header {
  line-height: 1.5;
  max-height: 100vh;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

nav {
  width: 100%;
  font-size: 12px;
  text-align: center;
  margin-top: 2rem;
}

nav a.router-link-exact-active {
  color: var(--color-text);
}

nav a.router-link-exact-active:hover {
  background-color: transparent;
}

nav a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}

nav a:first-of-type {
  border: 0;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  nav {
    text-align: left;
    margin-left: -1rem;
    font-size: 1rem;

    padding: 1rem 0;
    margin-top: 1rem;
  }
}
</style>-->

<template>
  <div id="app" class="container">
    <app-header></app-header>

    <app-new-game></app-new-game>

    <app-game-board></app-game-board>
  </div>
</template>

<script>
import Header from './components/Header.vue';
import NewGame from './components/NewGame.vue';
import GameBoard from './components/GameBoard.vue';

export default {
  name: 'App',
  components: {
      appHeader: Header,
      appNewGame: NewGame,
      appGameBoard: GameBoard
  }
}
</script>

<style>

</style>

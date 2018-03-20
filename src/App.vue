<template>
  <div id="app" class="container">
    <app-header></app-header>

    <app-new-game
            :matrix="matrix"
            @matrixChanged="matrix = $event"
    ></app-new-game>

    <app-game-board
            :matrix="newMatrix"
            @matrixChanged="matrix = $event"
    ></app-game-board>

  </div>
</template>

<script>
import Header from './components/Header.vue';
import NewGame from './components/NewGame.vue';
import GameBoard from './components/GameBoard.vue';

export default {
  name: 'App',
  data: function () {
      return {
          matrix: [
              [0,3,0,0],
              [0,0,0,0],
              [0,0,0,0],
              [0,0,0,0],
          ]
      }
  },
  computed: {
      newMatrix() {
          return this.matrix;
      }
  },
  components: {
      appHeader: Header,
      appNewGame: NewGame,
      appGameBoard: GameBoard
  }
}
</script>

<style>

</style>

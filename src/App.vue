<template>
  <div id="app" class="container">
    <app-header></app-header>

    <app-new-game
            :matrix="matrix"
            @matrixChanged="matrix = $event"
            ref="newGame"
    ></app-new-game>

    <app-game-board
            :matrix="matrix"
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
              [0,0,0,0],
              [0,0,0,0],
              [0,0,0,0],
              [0,0,0,0],
          ],
          row: '',
          column: ''
      }
  },
  methods: {

    addNewCell(event) {
        // if (event.key !== "ArrowRight" && event.key !== "ArrowLeft" && event.key !== "ArrowUp" && event.key !== "ArrowDown") {
        //     return;
        // }

        switch (event.key) {
            case "ArrowUp":
                this.arrowUpCase();
                break;
            case "ArrowDown":
                console.log(2);
                break;
            case "ArrowRight":
                console.log(3);
                break;
            case "ArrowLeft":
                console.log(4);
                break;
            default:
                console.log(5);
                return;
        }

        this.newCellNeeded();
    },
    newCellNeeded() {
        let intermediarMatrix = this.buildIntermediarMatrix();

        this.getRandomPairData();
        while(intermediarMatrix[this.row][this.column] !== 0 && this.fullMatrix() !== true) {
            this.getRandomPairData();
        }

        intermediarMatrix[this.row][this.column] = this.getRandomTwoOrFour();
        this.$nextTick(function () {
            this.matrix = intermediarMatrix;
        });
    },
    getRandomPairData() {
        this.row = Math.ceil(Math.random()*4) -1;
        this.column = Math.ceil(Math.random()*4) -1;
    },
    getRandomTwoOrFour() {
        return (Math.ceil(Math.random()*2)) * 2;
    },
    fullMatrix() {
        var state = true;
        dance:
        for (var i=0; i<this.matrix.length; i++) {
            for (var j=0; j< this.matrix.length; j++) {
                if (this.matrix[i][j] === 0) {
                    state = false;
                    break dance;
                }
            }
        }
        return state;
    },
    buildIntermediarMatrix() {
        let intermediarMatrix = [
            [0, 0, 0, 0],
            [0, 0, 0, 0],
            [0, 0, 0, 0],
            [0, 0, 0, 0],
        ];

        for (var i = 0; i < intermediarMatrix.length; i++) {
            for (var j = 0; j < intermediarMatrix.length; j++) {
                intermediarMatrix[i][j] = this.matrix[i][j];
            }
        }

        return intermediarMatrix;
    },
    arrowUpCase() {
        let mirror =  [
            [0, 0, 0, 0],
            [0, 0, 0, 0],
            [0, 0, 0, 0],
            [0, 0, 0, 0],
        ];

        let intermediarMatrix = this.buildIntermediarMatrix();
        let ok = '';
        console.log(intermediarMatrix);
        for(let j=0;j<4;++j) {
            for (let i = 1; i < 4; ++i) {
                if (intermediarMatrix[i][j] !== 0) {
                    let m = i - 1;

                    while (intermediarMatrix[m][j] === 0 && m >= 0) {
                        intermediarMatrix[m][j] = intermediarMatrix[m + 1][j];
                        intermediarMatrix[m + 1][j] = 0;
                        m--;
                        ok = 1;
                    }
                    if (m >= 0 && intermediarMatrix[m][j] === intermediarMatrix[m + 1][j] && mirror[m][j] !== 1) {
                        intermediarMatrix[m][j] = intermediarMatrix[m][j] + intermediarMatrix[m + 1][j];
                        intermediarMatrix[m + 1][j] = 0;
                        mirror[m][j] = 1;
                        ok = 1;
                    }
                }
            }
        }

        this.matrix = intermediarMatrix;

        if(ok === 1) {
            this.newCellNeeded();
        }

    }
  },
  components: {
      appHeader: Header,
      appNewGame: NewGame,
      appGameBoard: GameBoard
  },
  mounted() {
      this.$refs.newGame.newMatrix();
  },
    created: function () {
        window.addEventListener('keyup', this.addNewCell);
    },
}
</script>

<style>

</style>

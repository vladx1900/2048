<template>

    <div class="row">

        <div class="col-xs-7 text-right">
            <h4>Join the numbers and get to the <b>2048</b> tile!</h4>
        </div>

        <div class="col-xs-3 text-center">
            <button class="btn btn-primary" @click="newMatrix">New game</button>
        </div>


    </div>

</template>

<script>
    export default {
        props: ['matrix'],
        data: function () {
            return {
                row: '',
                column: ''
            }
        },
        methods: {
            newMatrix() {
                var intermediarMatrix =[[0,0,0,0],
                                        [0,0,0,0],
                                        [0,0,0,0],
                                        [0,0,0,0] ];
                this.getRandomPairData();
                intermediarMatrix[this.row][this.column] = this.getRandomTwoOrFour();
                this.getRandomPairData();
                while (intermediarMatrix[this.row][this.column] !== 0 ) {
                    this.getRandomPairData();
                }
                intermediarMatrix[this.row][this.column] = this.getRandomTwoOrFour();

                this.matrix = intermediarMatrix;
                this.$emit('matrixChanged', this.matrix);
            },
            getRandomPairData() {
                this.row = Math.ceil(Math.random()*4) -1;
                this.column = Math.ceil(Math.random()*4) -1;
            },
            getRandomTwoOrFour() {
                return (Math.ceil(Math.random()*2)) * 2;
            }
        }
    }
</script>

<style>

</style>
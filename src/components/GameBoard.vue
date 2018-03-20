<template>
    <div class="row text-center">


        <div class="" id="board" ref="board">

            <div class=" grid-row" v-for="rows in matrix">
                <div class=" grid-cell" v-for="columns in rows">

                    <app-cell v-if="columns !== 0" :value="columns"></app-cell>

                </div>
            </div>

        </div>


    </div>
</template>

<script>
    import Cell from './Cell.vue';

    export default {
        props: ['matrix'],
        data: function() {
            return {
                windowHeight: 0
            }
        },
        methods: {
            getWindowHeight(event) {
                this.windowHeight = this.$refs.board.clientWidth;
                this.$refs.board.setAttribute("style", "height: " + this.windowHeight + "px");
            },
            matrixChanged() {

                //this.$emit('marixChanged', this.matrix);
            }

        },
        computed: {
            matrixWasChanged() {
                console.log("comp");

                return this.matrix;
            }
        },
        mounted: function () {
            this.$nextTick(function () {

                this.$refs.board.setAttribute("style", "height: " + this.$refs.board.clientWidth + "px");

                window.addEventListener('resize', this.getWindowHeight);

                //Init
                this.getWindowHeight();
            })
        },
        beforeDestroy() {
            window.removeEventListener('resize', this.getWindowHeight);
        },
        components: {
            appCell: Cell
        }


    }

</script>

<style>
    #board {
        width: 50%;
        border: 1px solid;
        border-radius: 5px;
        margin-top: 5%;
        background-color: #676769c9;
        margin-right: 25%;
        margin-left: 25%;
    }

    .grid-row {
        height: 23%;
        width: 100%;
    }
    .grid-row:first-child {
        margin-top: 3.5%;
    }
    .grid-row:last-child {
        margin-bottom: 0;
    }

    .grid-cell {

        width: 20%;
        height: 88%;
        float: left;
        border-radius: 5px;
        background: darkgray;
        margin-right: 4%;
        margin-bottom: 4%;
    }
    .grid-cell:first-child {
        margin-left: 4%;
    }
    .grid-cell:last-child {
        margin-bottom: 0;
    }


</style>
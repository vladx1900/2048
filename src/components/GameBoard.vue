<template>
    <div class="row">

        <div class="col-xs-3"></div>
        <div class="col-xs-6" id="board" ref="board"></div>

    </div>
</template>

<script>
    export default {
        data: function() {
            return {
                windowHeight: 0
            }
        },
        methods: {

            getWindowHeight(event) {
                this.windowHeight = this.$refs.board.clientWidth;
                this.$refs.board.setAttribute("style", "height: " + this.windowHeight + "px");
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
        }


    }

</script>

<style>
    #board {
        width: 50%;
        height: 50%;
        border: 1px solid;
        margin-top: 10%;
    }

</style>
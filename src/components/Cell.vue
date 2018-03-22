<template>
    <div class="one-cell" ref="cellHeight">
        <p class="one-cell-number" :style="{lineHeight: oneCellHeight + 'px', fontSize: textSize + 'px'}">{{this.value}}</p>
    </div>
</template>

<script>
    export default {
        data: function () {
            return {
                oneCellHeight: '',
                textSize: ''
            }
        },
        props: [
            "value"
        ],
        methods: {
            changeCellHeight() {
                this.oneCellHeight = this.$refs.cellHeight.clientHeight;
                this.textSize = ( this.oneCellHeight * 35 ) / 100 ;
            }
        },
        mounted: function () {
            this.$nextTick(function () {

                this.changeCellHeight();

                window.addEventListener('resize', this.changeCellHeight);

            });
        }

    }
</script>

<style>
    .one-cell {
        background-color: beige;
        width: 100%;
        height: 100%;
        border-radius: 5px;
    }

    .one-cell-number {
        font-weight: bold;
        text-align: center;
    }
</style>
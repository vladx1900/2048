<template>
    <div class="one-cell">
        {{this.value}}
    </div>
</template>

<script>
    export default {
        props: [
            "value"
        ]
    }
</script>

<style>
    .one-cell {
        background-color: beige;
        width: 100%;
        height: 100%;
        border-radius: 5px;
    }
</style>
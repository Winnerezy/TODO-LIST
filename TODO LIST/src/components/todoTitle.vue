<script setup>
import {ref} from 'vue'
const title = ref('TODO')

</script>

<template>
    <div>
        <h1>{{ title }}</h1>
    </div>

</template>

<style scoped>
div{
    display: flex;
    align-items: center;
    justify-content: center;
}

h1{
    -webkit-text-fill-color: transparent;
    -webkit-text-stroke: 1px white;
    font-family: "Arial";
    letter-spacing: 10px;
}
</style>
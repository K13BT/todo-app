<template>
    <h2 
    :style="{color: darkMode ? 'hsl(233, 14%, 35%)' : 'hsl(233, 11%, 84%)'}"
    >Nothing left to do.</h2>
</template>


<script>
    export default {
        name: 'NoTodos',
        props: {
            darkMode: Boolean
        }
    }
</script>


<style scoped>
    h2 {
        padding: 100px;
        text-align: center;
        font-size: 40px;
        color: hsl(233, 14%, 35%);
    }

    @media (max-width: 1024px) {
        h2 {
            padding: 80px;
        }
    }

    @media (max-width: 525px) {
        h2 {
            padding: 60px;
        }
    }
</style>
<template>
    <div>
        <h1>TODO</h1>
        <button @click="$emit('toggle-mode')">
            <img :src="darkMode ? require('../assets/images/icon-sun.svg') : require('../assets/images/icon-moon.svg')" />
        </button>
    </div>
</template>


<script>
    export default {
        name: 'HeaderMode',
        props: {
            darkMode: Boolean
        },
        emits: ['toggle-mode']
    }
</script>


<style scoped>

div {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 30px;
}

button {
    background-color: transparent;
    border: none;
}

h1 {
    font-weight: bold;
    letter-spacing: 0.3em;
    color: hsl(0, 0%, 98%);
  }
</style>
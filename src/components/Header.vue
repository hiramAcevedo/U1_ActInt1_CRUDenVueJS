<!-- src/components/Header.vue -->
<template>
<header class="header">
    <div class="logo">Vue.js</div>
    <!-- Al pulsar, emite el evento para abrir el modal de stock -->
    <button class="consult-btn" @click="$emit('open-stock')">Consultar</button>
</header>
</template>

<script>
export default {
name: "Header"
}
</script>

<style scoped>
.header {
display: flex;
justify-content: space-between;
align-items: center;
background-color: #42b983;
color: white;
padding: 10px 20px;
}
.logo {
font-size: 1.5em;
font-weight: bold;
}
.consult-btn {
background-color: #fff;
color: #42b983;
border: none;
padding: 8px 12px;
border-radius: 4px;
cursor: pointer;
}
</style>  
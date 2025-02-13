<!-- src/components/AddedProductsModal.vue -->
<template>
<div class="modal">
<div class="modal-content">
    <h2>Productos Añadidos</h2>
    <div class="success-message">
    <p>¡Los productos han sido añadidos exitosamente!</p>
    </div>
    <div class="table-wrapper">
    <table class="added-products-table">
        <thead>
        <tr>
            <th>Producto</th>
            <th>Descripción</th>
            <th>Categoría</th>
            <th>Stock</th>
            <th>Precio</th>
        </tr>
        </thead>
        <tbody>
        <tr v-for="(item, index) in newProducts" :key="index">
            <td>{{ item.name }}</td>
            <td>{{ item.description }}</td>
            <td>{{ item.category }}</td>
            <td>{{ item.stock }}</td>
            <td>{{ item.price }}</td>
        </tr>
        </tbody>
    </table>
    </div>
    <div class="modal-actions">
    <button @click="viewStock">Ver Productos en Stock</button>
    <button @click="exit">Salir</button>
    </div>
</div>
</div>
</template>

<script>
export default {
name: "AddedProductsModal",
props: {
newProducts: {
    type: Array,
    default: () => []
}
},
methods: {
viewStock() {
    this.$emit('view-stock');
},
exit() {
    this.$emit('exit');
}
}
}
</script>

<style scoped>
.modal {
position: fixed;
top: 0;
left: 0;
width: 100%;
height: 100%;
background-color: rgba(0,0,0,0.5);
display: flex;
justify-content: center;
align-items: center;
}
.modal-content {
background-color: white;
padding: 20px;
width: 800px;
max-height: 80vh;
overflow-y: auto;
border-radius: 8px;
box-sizing: border-box;
}
.success-message {
text-align: center;
margin: 20px 0;
padding: 20px;
background-color: #f0f7f4;
border-radius: 4px;
}
.success-message p {
color: #42b983;
font-size: 1.2em;
margin: 0;
}
.table-wrapper {
max-height: 400px;
overflow-y: auto;
margin-bottom: 10px;
}
.added-products-table {
width: 100%;
border-collapse: collapse;
}
.added-products-table th,
.added-products-table td {
border: 1px solid #ddd;
padding: 8px;
text-align: left;
}
.added-products-table th {
background-color: #f2f2f2;
}
.modal-actions {
text-align: right;
margin-top: 10px;
}
.modal-actions button {
padding: 6px 12px;
margin-left: 10px;
border: none;
border-radius: 4px;
cursor: pointer;
}
</style>
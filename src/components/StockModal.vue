<!-- src/components/StockModal.vue -->
<template>
<div class="modal">
    <div class="modal-content">
    <h2>Productos en Stock</h2>
    <div class="table-wrapper">
        <table class="stock-table">
            <thead>
                <tr>
                <th>ID</th>
                <th>Producto</th>
                <th>Descripción</th>
                <th>Categoría</th>
                <th>Stock</th>
                <th>Precio</th>
                </tr>
            </thead>
            <tbody>
            <tr v-for="product in products" :key="product.id">
                <td>{{ product.id }}</td>
                <td>{{ product.name }}</td>
                <td>{{ product.description }}</td>
                <td>{{ product.category }}</td>
                <td>{{ product.stock }}</td>
                <td>{{ product.price }}</td>
            </tr>
            </tbody>
        </table>
    </div>
    <div class="modal-actions">
        <button @click="$emit('close-stock-modal')">Cerrar</button>
    </div>
    </div>
</div>
</template>

<script>
export default {
name: "StockModal",
props: {
    products: {
    type: Array,
    default: () => []
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
width: 600px;
max-height: 80vh;
overflow-y: auto;
border-radius: 8px;
}
.table-wrapper {
max-height: 300px;
overflow-y: auto;
margin-bottom: 10px;
}
.stock-table {
width: 100%;
border-collapse: collapse;
}
.stock-table th,
.stock-table td {
border: 1px solid #ddd;
padding: 6px;
}
.modal-actions {
text-align: right;
margin-top: 10px;
}
.modal-actions button {
padding: 6px 12px;
border: none;
border-radius: 4px;
cursor: pointer;
}
</style>  
<!-- src/components/InventoryTable.vue -->
<template>
<div class="table-container">
    <table class="inventory-table">
    <thead>
        <tr>
        <th>ID</th>
        <th>Producto</th>
        <th>Descripción</th>
        <th>Categoría</th>
        <th>Stock</th>
        <th>Precio</th>
        <th>Acciones</th>
        </tr>
    </thead>
    <tbody>
        <tr v-for="(product, index) in products" :key="product.id">
        <td>{{ product.id }}</td>
        <td>
            <div v-if="editingIndex === index">
            <input type="text" v-model="tempProduct.name" />
            </div>
            <div v-else>
            {{ product.name }}
            </div>
        </td>
        <td>
            <div v-if="editingIndex === index">
            <input type="text" v-model="tempProduct.description" />
            </div>
            <div v-else>
            {{ product.description }}
            </div>
        </td>
        <td>
            <div v-if="editingIndex === index">
            <input type="text" v-model="tempProduct.category" />
            </div>
            <div v-else>
            {{ product.category }}
            </div>
        </td>
        <td>
            <div v-if="editingIndex === index">
            <input type="number" v-model.number="tempProduct.stock" />
            </div>
            <div v-else>
            {{ product.stock }}
            </div>
        </td>
        <td>
            <div v-if="editingIndex === index">
            <input type="number" v-model.number="tempProduct.price" step="0.01" />
            </div>
            <div v-else>
            {{ product.price }}
            </div>
        </td>
        <td>
            <div v-if="editingIndex === index">
            <button @click="saveEdit(index)">Guardar</button>
            <button @click="cancelEdit()">Cancelar</button>
            </div>
            <div v-else>
            <button class="edit-btn" @click="startEdit(index)">Editar</button>
            <button class="delete-btn" @click="$emit('delete-product', index)">Eliminar</button>
            </div>
        </td>
        </tr>
    </tbody>
    </table>
</div>
</template>

<script>
export default {
name: "InventoryTable",
props: {
    products: {
    type: Array,
    required: true
    }
},
data() {
    return {
    editingIndex: null,
    tempProduct: {}
    }
},
methods: {
    startEdit(index) {
    this.editingIndex = index;
    // Creamos una copia del producto para editarlo sin modificar la lista original
    this.tempProduct = { ...this.products[index] };
    },
    saveEdit(index) {
    // Emitimos el producto actualizado junto con su índice
    this.$emit('update-product', index, this.tempProduct);
    this.editingIndex = null;
    this.tempProduct = {};
    },
    cancelEdit() {
    this.editingIndex = null;
    this.tempProduct = {};
    }
}
}
</script>

<style scoped>
.table-container {
max-width: 1280px;
margin: 20px auto;
}
.inventory-table {
width: 100%;
border-collapse: collapse;
}
.inventory-table th,
.inventory-table td {
border: 1px solid #ddd;
padding: 8px;
text-align: left;
}
.inventory-table th {
background-color: #f2f2f2;
}
.edit-btn, .delete-btn {
padding: 6px 10px;
margin: 2px;
border: none;
border-radius: 4px;
cursor: pointer;
}
.edit-btn {
background-color: #ffcc00;
color: black;
}
.delete-btn {
background-color: #ff4d4d;
color: white;
}
</style>  
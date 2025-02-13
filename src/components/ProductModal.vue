<!-- src/components/ProductModal.vue -->
<template>
<div class="modal">
    <div class="modal-content">
    <h2>Añadir Productos en Lote</h2>
    <div class="table-wrapper">
        <table class="modal-table">
        <thead>
            <tr>
            <th>Producto</th>
            <th>Descripción</th>
            <th>Categoría</th>
            <th>Stock</th>
            <th>Precio</th>
            <th>Acciones</th>
            </tr>
        </thead>
        <tbody>
            <tr v-for="(item, index) in newProducts" :key="index">
            <td><input type="text" v-model="item.name" placeholder="Nombre" required></td>
            <td><input type="text" v-model="item.description" placeholder="Descripción" required></td>
            <td><input type="text" v-model="item.category" placeholder="Categoría" required></td>
            <td><input type="number" v-model.number="item.stock" placeholder="Stock" required></td>
            <td><input type="number" v-model.number="item.price" placeholder="Precio" step="0.01" required></td>
            <td><button @click="removeRow(index)">Eliminar Fila</button></td>
            </tr>
        </tbody>
        </table>
    </div>
    <button @click="addRow" class="add-row-btn">Añadir Fila</button>
    <div class="modal-actions">
        <button @click="handleSave">Guardar</button>
        <button @click="closeModal">Cancelar</button>
    </div>
    </div>
</div>
</template>

<script>
export default {
name: "ProductModal",
data() {
    return {
    newProducts: [
        { name: '', description: '', category: '', stock: 0, price: 0 }
    ]
    }
},
methods: {
    addRow() {
    this.newProducts.push({ name: '', description: '', category: '', stock: 0, price: 0 });
    },
    removeRow(index) {
    this.newProducts.splice(index, 1);
    if (this.newProducts.length === 0) {
        this.addRow();
    }
    },
    handleSave() {
    const validProducts = this.newProducts.filter(product => product.name.trim() !== '');
    if (validProducts.length > 0) {
        // Emitimos los productos válidos para confirmar
        this.$emit('confirm-products', validProducts);
        this.resetForm();
    } else {
        alert("Debe ingresar al menos un producto con nombre.");
    }
    },
    closeModal() {
    this.resetForm();
    this.$emit('close-modal');
    },
    resetForm() {
    this.newProducts = [{ name: '', description: '', category: '', stock: 0, price: 0 }];
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
width: 1000px; /* Ventana lo suficientemente ancha para evitar scroll horizontal */
max-height: 80vh;
overflow-y: auto;
border-radius: 8px;
box-sizing: border-box;
}
.table-wrapper {
max-height: 400px;
overflow-y: auto;
margin-bottom: 10px;
}
.modal-table {
width: 100%;
border-collapse: collapse;
}
.modal-table th,
.modal-table td {
border: 1px solid #ddd;
padding: 6px;
text-align: left;
}
.add-row-btn {
background-color: #42b983;
color: white;
padding: 6px 10px;
border: none;
border-radius: 4px;
cursor: pointer;
margin-bottom: 10px;
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
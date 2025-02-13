<!-- src/App.vue -->
<template>
  <div id="app">
    <!-- Header: al pulsar “Consultar” se abre el modal de stock -->
    <Header @open-stock="() => { showStockModal = true }" />
    <main>
      <div class="top-bar">
        <h1>Sistema de Inventario de Productos</h1>
        <!-- Botón "+" para abrir el modal de agregar productos en lote -->
        <button class="add-product-btn" @click="openProductModal">+</button>
      </div>

      <!-- Tabla de inventario con edición en línea -->
      <InventoryTable 
        v-if="!showStockModal" 
        :products="products" 
        @delete-product="deleteProduct"
        @update-product="updateProduct" />

      <!-- Modal para agregar productos en lote -->
      <ProductModal 
        v-if="showModal" 
        @confirm-products="handleConfirmProducts"
        @close-modal="closeProductModal" />

      <!-- Modal para confirmar productos añadidos -->
      <AddedProductsModal 
        v-if="showAddedModal" 
        :newProducts="pendingNewProducts" 
        @view-stock="handleAddedModalViewStock"
        @exit="handleAddedModalExit" />

      <!-- Modal para ver productos en stock -->
      <StockModal 
        v-if="showStockModal" 
        :products="filteredProducts" 
        @close-stock-modal="closeStockModal" />
    </main>
  </div>
</template>

<script>
import Header from './components/Header.vue'
import InventoryTable from './components/InventoryTable.vue'
import ProductModal from './components/ProductModal.vue'
import AddedProductsModal from './components/AddedProductsModal.vue'
import StockModal from './components/StockModal.vue'

export default {
  name: 'App',
  components: {
    Header,
    InventoryTable,
    ProductModal,
    AddedProductsModal,
    StockModal
  },
  data() {
    return {
      products: [],           // Lista global de productos
      showModal: false,       // Modal para agregar productos en lote
      showAddedModal: false,  // Modal de confirmación de productos añadidos
      showStockModal: false,  // Modal para ver productos en stock
      nextId: 1,              // Para asignar IDs únicos
      pendingNewProducts: []  // Almacena temporalmente los productos nuevos
    }
  },
  computed: {
    // Filtra los productos que tienen stock mayor a 0
    filteredProducts() {
      return this.products.filter(product => product.stock > 0);
    }
  },
  methods: {
    openProductModal() {
      this.showModal = true;
    },
    closeProductModal() {
      this.showModal = false;
    },
    // Al recibir nuevos productos desde ProductModal, se almacenan para confirmar
    handleConfirmProducts(newProducts) {
      this.pendingNewProducts = newProducts;
      this.showModal = false;
      this.showAddedModal = true;
    },
    // Al salir de la confirmación, se agregan los productos a la lista global y se cierra el modal
    handleAddedModalExit() {
      this.pendingNewProducts.forEach(product => {
        this.products.push({
          id: this.nextId++,
          ...product
        });
      });
      this.pendingNewProducts = [];
      this.showAddedModal = false;
    },
    // Al seleccionar "Ver Productos en Stock", se agrega y se abre el modal de stock
    handleAddedModalViewStock() {
      this.handleAddedModalExit();
      this.showStockModal = true;
    },
    closeStockModal() {
      this.showStockModal = false;
    },
    updateProduct(index, updatedProduct) {
      this.products.splice(index, 1, updatedProduct);
    },
    deleteProduct(index) {
      if (confirm('¿Está seguro de eliminar este producto?')) {
        this.products.splice(index, 1);
      }
    }
  }
}
</script>

<style scoped>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  margin: 0; /* Eliminamos márgenes para evitar el marco blanco en el header */
  padding: 0;
}
.top-bar {
  display: flex;
  justify-content: space-around;
  align-items: center;
  margin: 20px;
}
.add-product-btn {
  background-color: #42b983;
  color: white;
  border: none;
  font-size: 1.5em;
  width: 40px;
  height: 40px;
  border-radius: 50%;
  cursor: pointer;
}
</style>
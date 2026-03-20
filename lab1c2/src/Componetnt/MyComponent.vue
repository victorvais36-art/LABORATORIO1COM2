<script setup lang="ts">
import { ref, computed } from 'vue'

// --- 1. Definición del Menú ---
const menu = ref([
  { id: 1, nombre: 'Burger Clásica', precio: 5.50, icono: '🍔' },
  { id: 2, nombre: 'CheeseBurger', precio: 6.25, icono: '🧀' },
  { id: 3, nombre: 'Burger Doble', precio: 8.00, icono: '🥓' },
  { id: 4, nombre: 'Papas Chicas', precio: 2.50, icono: '🍟' },
  { id: 5, nombre: 'Papas Medianas', precio: 3.25, icono: '🍟' },
  { id: 6, nombre: 'Papas Grandes', precio: 4.00, icono: '🍟' },
  { id: 7, nombre: 'Soda Refresco', precio: 1.50, icono: '🥤' }
])

// --- 2. Estado del Carrito ---
interface ItemCarrito {
  id: number
  nombre: string
  precio: number
  cantidad: number
}

const carrito = ref<ItemCarrito[]>([])

// --- 3. Lógica de Funciones ---
const agregarAlCarrito = (producto: any) => {
  const itemExistente = carrito.value.find(item => item.id === producto.id)
  if (itemExistente) {
    itemExistente.cantidad++
  } else {
    carrito.value.push({
      ...producto,
      cantidad: 1
    })
  }
}

const eliminarDelCarrito = (index: number) => {
  carrito.value.splice(index, 1)
}

const finalizarVenta = () => {
  if (carrito.value.length === 0) return
  alert(`Venta realizada con éxito por $${totalCart.value.toFixed(2)}`)
  carrito.value = []
}

// --- 4. Propiedades Computadas ---
const totalCart = computed(() => {
  return carrito.value.reduce((acc, item) => acc + (item.precio * item.cantidad), 0)
})
</script>

<template>
  <div class="pos-container">
    <header class="header">
      <h1>🍔 Burger POS</h1>
    </header>

    <div class="main-layout">
      <section class="menu-grid">
        <div 
          v-for="prod in menu" 
          :key="prod.id" 
          class="product-card" 
          @click="agregarAlCarrito(prod)"
        >
          <span class="icon">{{ prod.icono }}</span>
          <h3>{{ prod.nombre }}</h3>
          <p class="price">${{ prod.precio.toFixed(2) }}</p>
        </div>
      </section>

      <aside class="ticket-aside">
        <h2>Detalle de Venta</h2>
        
        <div v-if="carrito.length === 0" class="empty-msg">
          Carrito vacío
        </div>

        <div v-else class="ticket-list">
          <div v-for="(item, index) in carrito" :key="index" class="ticket-item">
            <div class="item-info">
              <span class="qty">{{ item.cantidad }}x</span>
              <span class="name">{{ item.nombre }}</span>
            </div>
            <div class="item-price">
              ${{ (item.precio * item.cantidad).toFixed(2) }}
              <button @click.stop="eliminarDelCarrito(index)" class="btn-del">×</button>
            </div>
          </div>

          <div class="total-section">
            <div class="total-row">
              <span>TOTAL:</span>
              <span class="total-amount">${{ totalCart.toFixed(2) }}</span>
            </div>
            <button @click="finalizarVenta" class="btn-pay">Pagar Ahora</button>
          </div>
        </div>
      </aside>
    </div>
  </div>
</template>

<style scoped>
.pos-container {
  font-family: sans-serif;
  max-width: 1000px;
  margin: 0 auto;
  color: #333;
}

.header {
  text-align: center;
  padding: 20px;
  background: #f39c12;
  color: white;
  border-radius: 8px;
  margin-bottom: 20px;
}

.main-layout {
  display: grid;
  grid-template-columns: 1fr 350px;
  gap: 20px;
}

/* Grid de productos */
.menu-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(140px, 1fr));
  gap: 15px;
}

.product-card {
  background: #fff;
  border: 1px solid #ddd;
  border-radius: 10px;
  padding: 15px;
  text-align: center;
  cursor: pointer;
  transition: transform 0.1s;
}

.product-card:active {
  transform: scale(0.95);
}

.icon {
  font-size: 2.5rem;
  display: block;
  margin-bottom: 10px;
}

.price {
  font-weight: bold;
  color: #e67e22;
}

/* Estilos del Ticket */
.ticket-aside {
  background: #f9f9f9;
  border: 2px dashed #ccc;
  padding: 20px;
  border-radius: 8px;
  height: fit-content;
}

.ticket-item {
  display: flex;
  justify-content: space-between;
  padding: 10px 0;
  border-bottom: 1px solid #eee;
  font-size: 0.9rem;
}

.qty {
  font-weight: bold;
  margin-right: 10px;
  color: #7f8c8d;
}

.btn-del {
  background: none;
  border: none;
  color: #e74c3c;
  cursor: pointer;
  font-weight: bold;
  margin-left: 10px;
}

.total-section {
  margin-top: 20px;
  border-top: 2px solid #333;
  padding-top: 15px;
}

.total-row {
  display: flex;
  justify-content: space-between;
  font-weight: bold;
  font-size: 1.2rem;
  margin-bottom: 15px;
}

.total-amount {
  color: #27ae60;
}

.btn-pay {
  width: 100%;
  padding: 12px;
  background: #27ae60;
  color: white;
  border: none;
  border-radius: 5px;
  font-weight: bold;
  cursor: pointer;
}

.btn-pay:hover {
  background: #219150;
}

.empty-msg {
  text-align: center;
  color: #999;
  padding: 30px;
}
</style>
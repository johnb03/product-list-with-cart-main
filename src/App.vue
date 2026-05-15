<script setup>
import { reactive, provide, ref } from 'vue'
import CardsProduct from './components/cardsProduct.vue'
import Cartamount from './components/cart.vue'
import Products from '../data.json'
import ModalConfirm from './components/modalConfirm.vue'
const showModal = ref(false)
function confirmOrder() {
  showModal.value = true
}
const cart = reactive({
  items: [],
  totalItems: 0,
  totalPrice: 0,
})
// add product to cart
function addCard(product) {
  console.log('addCard,called', product)
  const existing = cart.items.find((item) => item.name === product.name)

  if (existing) {
    existing.quantity++
    cart.totalItems++
    cart.totalPrice += product.price
  } else {
    cart.items.push({ name: product.name, price: product.price, quantity: 1, image: product.image })
    console.log('cart items after:', JSON.stringify(cart.items))
    cart.totalItems++
    cart.totalPrice += product.price
  }
}
// increment product in the cart
function increment(product) {
  const existing = cart.items.find((item) => item.name === product.name)
  if (existing) {
    existing.quantity++
    cart.totalItems++
    cart.totalPrice += product.price
  }
}
// decrement product in the cart
function decrement(product) {
  const existing = cart.items.find((item) => item.name === product.name)
  if (existing) {
    existing.quantity--
    cart.totalItems--
    cart.totalPrice -= product.price

    if (existing.quantity === 0) {
      cart.items = cart.items.filter((item) => item.quantity > 0)
    }
  }
}

// function delete items
function deleteItems(product) {
  const deleteItem = cart.items.find((item) => item.name === product.name)
  if (deleteItem) {
    cart.totalItems -= deleteItem.quantity
    cart.totalPrice -= deleteItem.price * deleteItem.quantity
    cart.items = cart.items.filter((item) => item.name !== product.name)
  }
}

// funtion star new order
function startNewOrder() {
  if (startNewOrder) {
    showModal.value = false
    cart.items = []
    cart.totalItems = 0
    cart.totalPrice = 0
  }
}

provide('cart', {
  cart,
  addCard,
  increment,
  decrement,
  deleteItems,
  showModal,
  confirmOrder,
  startNewOrder,
})
</script>

<template class="relative">
  <ModalConfirm v-if="showModal" />
  <div class="grid grid-cols-1 md:grid-cols-3 bg-rose-50 p-4" id="content">
    <div
      class="w-full flex flex-col md:flex-row md:col-span-2 md:flex-wrap gap-4 items-center"
      id="content-right"
    >
      <h2 class="text-4xl w-72 text-left font-bold md:w-full">Desserts</h2>
      <CardsProduct
        v-for="(item, index) in Products"
        :key="index"
        :product="item.category"
        :nameProduct="item.name"
        :price="item.price"
        :imageUrl="item.image"
      />
    </div>
    <div class="mt-4 flex justify-center md:self-start" id="content-left">
      <Cartamount />
    </div>
  </div>
</template>
<style scoped></style>

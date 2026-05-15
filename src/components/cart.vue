<script setup>
import { inject } from 'vue'
const { cart, deleteItems, confirmOrder } = inject('cart')
</script>
<!--  Se injectaran  los articulos -->
<!-- agregados al carrio en cartAmoutnt -->
<template>
  <div class="w-72 p-6 bg-rose-100 rounded-md" id="cart">
    <h2 class="text-red font-bold" id="cart-tiitle">
      You Cart ( <span>{{ cart.totalItems }}</span> )
    </h2>

    <div v-if="cart.items.length === 0" id="cart-view__empty" class="">
      <img
        class="rounded-md block ml-auto mr-auto"
        src="../assets/images/illustration-empty-cart.svg "
        alt="empty cart"
      />
      <p class="text-gray-400 text-xs">You added items will appear here</p>
    </div>
    <!-- item in the cart -->
    <!-- div main cart -->
    <div class="bg-rose-100 rounded-md">
      <!-- div items  -->
      <div
        class="flex pt-4 gap-2 justify-between border-t-2 border-gray-200"
        v-for="item in cart.items"
        :key="item.id"
      >
        <!-- item title -->
        <div class="flex flex-col gap-2">
          <h4 class="text-xs">{{ item.name }}</h4>
          <!-- ---- -->

          <div class="flex gap-4 text-xs">
            <!-- item quantity -->
            <p class="text-rose-600">{{ item.quantity }}X</p>
            <!-- item price -->
            <p class="text-gray-600">${{ item.price }}</p>
            <p class="text-gray-600">
              <!-- item total price -->
              ${{ (item.price * item.quantity).toFixed(2) }}
            </p>
          </div>
          <!-- ----- -->
        </div>
        <!-- delete selected items -->
        <button
          @click="deleteItems(item)"
          class="w-3 h-3 cursor-pointer rounded-full border border-gray-400 hover:border-black"
        >
          <svg
            class="fill-gray-400 hover:fill-black"
            xmlns="http://www.w3.org/2000/svg"
            width="10"
            height="10"
            fill="none"
            viewBox="0 0 10 10"
          >
            <path
              d="M8.375 9.375 5 6 1.625 9.375l-1-1L4 5 .625 1.625l1-1L5 4 8.375.625l1 1L6 5l3.375 3.375-1 1Z"
            />
          </svg>
        </button>
      </div>

      <div class="mt-10" v-if="cart.items.length > 0" id="cart-TotalOrder">
        <div class="flex justify-between items-center">
          <p class="text-xs text-gray-600">Order Total</p>
          <span class="font-bold text-xl">${{ cart.totalPrice.toFixed(2) }}</span>
        </div>
        <span class="flex gap-1 pt-6 text-xs align-middle"
          ><img src="../assets/images/icon-carbon-neutral.svg" alt="carbon neutral" /> This is
          carbon-neutral delivery</span
        >
      </div>
      <!-- confirm order -->
      <button
        @click="confirmOrder"
        class="w-60 bg-red mt-4 text-white pt-2 pb-2 pl-5 pr-5 rounded-3xl hover:cursor-pointer transition-transform active:scale-95"
        v-if="cart.items.length > 0"
      >
        Confirm Order
      </button>
    </div>
  </div>
</template>

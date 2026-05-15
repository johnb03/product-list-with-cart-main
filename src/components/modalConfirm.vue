<script setup>
import { inject } from 'vue'

const { startNewOrder, cart } = inject('cart')
</script>

<template>
  <div class="w-full h-dvh bg-black/50 fixed inset-0 flex justify-center items-center z-20">
    <div
      class="w-full h-dvh mt-32 md:w-auto md:p-4 md:h-auto md:m-0 flex flex-col gap-4 bg-rose-50 rounded-2xl"
    >
      <div id="modal-title" class="w-60 h-50 p-3 flex flex-col justify-around">
        <img
          class="w-10 mt-4 mb-5"
          src="../assets/images/icon-order-confirmed.svg"
          alt="confimed"
        />

        <h2 class="font-extrabold text-4xl text-wrap">Order Confirmed</h2>
        <p class="text-xs text-gray-600 pl-0.5">We hope you enjoy your food!</p>
      </div>
      <div id="modal-wrap__product" class="max-h-60 overflow-y-auto">
        <div
          class="flex pt-4 gap-2 justify-between border-t-2 border-gray-200"
          v-for="item in cart.items"
          :key="item.name"
        >
          <!-- item title -->
          <div class="flex flex-col gap-2">
            <h4 class="text-xs">{{ item.name }}</h4>
            <!-- ---- -->

            <div class="flex items-center gap-4 text-xs">
              <div class="p-4 m-0">
                <img class="w-12" :src="item.image" alt=" product selected" />
              </div>
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
        </div>
        <div class="flex justify-between items-center pt-4 border-t-2 border-gray-200">
          <p class="text-xs text-gray-600">Order Total</p>
          <span class="font-bold text-xl">${{ cart.totalPrice.toFixed(2) }}</span>
        </div>
      </div>
      <div class="w-full flex justify-center">
        <button
          @click="startNewOrder"
          class="w-80 mt-5 mb-5 bg-rose-600 rounded-3xl text-white text-md font-bold pt-3 pb-3 pl-5 pr-5 transition-transform active:scale-95"
        >
          Start New Order
        </button>
      </div>
    </div>
  </div>
</template>

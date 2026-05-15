<script setup>
import { provide, inject, computed, ref } from 'vue'
const { cart, addCard, increment, decrement } = inject('cart')
const itemCart = computed(() => {
  return cart.items.find((item) => item.name === props.nameProduct)
})

const props = defineProps({
  product: String,
  nameProduct: String,
  price: Number,
  imageUrl: {
    type: Object,
    required: true,
    default: () => ({
      thumbnail: '',
      mobile: '',
      tablet: '',
      desktop: '',
    }),
  },
})
</script>

<!-- * template -->
<template>
  <div id="card" class="w-72 flex flex-col gap-6">
    <!-- hero card -->
    <div id="card-hero" class="flex flex-col content-center relative">
      <!-- image card -->
      <div>
        <picture class="">
          <source media="(min-width: 1024px)" :srcset="imageUrl.desktop" />
          <source media="(min-width: 768px)" :srcset="imageUrl.tablet" />
          <source media="(min-width: 480px)" :srcset="imageUrl.mobile" />
          <img
            :src="imageUrl.thumbnail"
            alt="product"
            class="w-full h-52 object-cover rounded-md block"
            :class="itemCart ? 'itemActive' : ''"
          />
        </picture>
      </div>

      <!-- button add cart -->
      <div
        :class="itemCart ? 'border-none' : ''"
        class="absolute right-23 -bottom-5 bg-rose-100 border-2 border-gray-500 w-28 rounded-4xl overflow-hidden"
      >
        <!-- boton de agregar al carito -->
        <button
          @click="addCard({ name: nameProduct, price: price, image: imageUrl.thumbnail })"
          v-if="!itemCart"
          id="addCart"
          class="w-full flex justify-center align-middle pt-2 pb-2 pl-2 pr-2 gap-2 text-xs cursor-pointer transition-transform active:scale-95"
        >
          <img src="/assets/images/icon-add-to-cart.svg" alt="cart" class="w-4" />
          Add Cart
        </button>
        <!-- fin botton add cart -->
        <!-- boton de mass y menos -->
        <div
          v-if="itemCart"
          id="card-button__moreLess"
          class="bg-red text-rose-50 w-full flex justify-between align-middle pt-1 pb-1 pl-2 pr-2"
        >
          <!-- boton de decrement -->
          <button @click="decrement({ name: nameProduct, price: price })" class="cursor-pointer">
            <img
              class="cursor-pointer"
              src="/assets/images/icon-decrement-quantity.svg"
              alt="decrement icon"
            />
          </button>
          <p>{{ itemCart.quantity }}</p>
          <!-- fin de boton decrement -->
          <!-- boton de increment -->
          <button @click="increment({ name: nameProduct, price: price })" class="cursor-pointer">
            <img
              class="cursor-pointer"
              src="/assets/images/icon-increment-quantity.svg"
              alt="Increment icon"
            />
          </button>
          <!-- fin de boton increment -->
        </div>
      </div>
    </div>

    <!-- descripcion del producto -->
    <div id="description">
      <p class="text-gray-500 text-xs" id="product">{{ props.nameProduct }}</p>
      <h4 id="nameProduct">{{ props.nameProduct }}</h4>
      <p class="text-red" id="price">$ {{ props.price }}</p>
    </div>
  </div>
</template>

<style scoped>
.itemActive {
  border: solid 2px rgb(199, 58, 15);
}
</style>

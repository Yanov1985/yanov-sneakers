<script setup>
import DrawerHead from './DrawerHeadComponent.vue'
import CartList from './CartList.vue'
</script>

<template>
  <div class="fixed top-0 left-0 h-full w-full bg-black z-10 opacity-70"></div>
  <div class="bg-white w-96 h-full fixed right-0 top-0 z-20 p-8">
    <!-- Вверхняя часть drawera -->
    <DrawerHead />
    <!-- Элемент корзины -->
    <CartList />

    <!-- Итоговая цена -->
    <div class="flex gap-2 my-7">
      <span>Итого:</span>
      <div class="flex-1 border-b border-dashed"></div>
      <b>12900 руб</b>
    </div>

    <!-- Кнопка заказа товара -->
    <button 
    disabled=""
    class="transition bg-lime-500 w-full rounded-xl py-3 mt-6 text-white disabled:bg-slate-300 hover:bg-lime-600 active:bg-lime-700 cursor-pointer">
      Оформить заказ
    </button>

  </div>
</template>

<script setup>
import Card from './Card.vue'

defineProps({
  products: Array
})

</script>

<template>
  <div class="p-10">    
    <div class="grid grid-cols-4 gap-5" v-auto-animate>
      <Card
      v-for="product in products"
      :key="product.id"
      :title="product.title"
      :image="product.image"
      :price="product.price"
      :isFavorites="product.isFavorites"
      />      
    </div>
  </div>
</template>

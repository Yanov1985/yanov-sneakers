<script setup>
import { onMounted, ref, reactive, watch } from 'vue'
import axios from 'axios'

import Header from './components/Header.vue'
import CardList from './components/CardList.vue'
// import Drawer from './components/DrawerComponent.vue'

//  Переменная товаров
const products = ref([])

// Парамметры поиска и сортировки
const filters = reactive({
  sortBy: 'title',
  searchQuery: ''
})

const onChangeSearchInput = (event) => {
  filters.searchQuery = event.target.value
}

const onChangeSelect = (event) => {
  filters.sortBy = event.target.value
}

// Функционал "Избарнного"
const fetchFavorites = async () => {
  try {
    const { data: favorites } = await axios.get('https://78697b69b96df617.mokky.dev/favorites')
    // Синхронизирует с переменной
    products.value = products.value.map(product => {
      const favorite = favorites.find(favorite => favorite.parentId === product.id);

      if (!favorite) {
        return product;
      }

      return {
        ...product,
        isFavorite: true,
        favoriteId: favorite.id,
      }
    });
  } catch (err) {
    console.log(err)
  }
}

// Добавления в избарнное
const addToFavorite = async (product) => {

  product.isFavorite = true;
}

// Рендер с сервера списка товаров
const fetchItems = async () => {
  try {
    const params = {
      sortBy: filters.sortBy
    }

    if (filters.searchQuery) {
      params.title = `*${filters.searchQuery}*`
    }

    const { data } = await axios.get('https://78697b69b96df617.mokky.dev/products', {
      params
    })
    // Синхронизирует с переменной
    products.value = data.map(obj => ({
      ...obj,
      isFavorite: false,
      isAdded: false
    }));
  } catch (err) {
    console.log(err)
  }
}

onMounted(async () => {
  await fetchItems();
  await fetchFavorites();
})
watch(filters, fetchItems)
</script>

<template>
  <!-- Корзина товара -->
  <!-- <Drawer /> -->
  <div class="bg-white w-4/5 m-auto rounded-xl shadow-xl mt-14">
    <!-- Шапка сайта -->
    <Header />

    <!-- Блок фильторов товара -->
    <div class="pr-10 pl-10 pt-10">
      <div class="flex justify-between items-center">
        <h2 class="text-3xl font-bold mb-8">Все крассовки</h2>

        <div class="flex gap-4">
          <!-- Фильтр -->
          <select @change="onChangeSelect" class="py-2 px-3 border rounded-md outline-none">
            <option value="title">По названию</option>
            <option value="price">По цене (дешевые)</option>
            <option value="-price">По цене (дорогие)</option>
          </select>

          <!-- Кнопка поиска -->
          <div class="relative">
            <img class="absolute left-4 top-3" src="/search.svg" alt="Search" />
            <input
              @input="onChangeSearchInput"
              class="border rounded-md py-2 pl-11 pr-4 outline-none focus:border-gray-400"
              placeholder="поиск..."
            />
          </div>
        </div>
      </div>
    </div>

    <!-- Карточка товара -->
    <CardList :products="products" />
  </div>
</template>

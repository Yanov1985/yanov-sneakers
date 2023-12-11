<template>
  <header class="flex justify-between border-b border-slate-200 px-10 py-8">
    <!-- Левая часть Header -->
    <div class="flex items-center gap-4">
      <img src="/logo.png" alt="logo" />
      <div>
        <h2 class="text-xl font-bold uppercase">Yanov Sneakers</h2>
        <p class="text-slate-400">Магазин лучших красовок</p>
      </div>
    </div>

    <!-- Меню  -->
    <ul class="flex items-center gap-10">
      <li class="flex items-center cursor-pointer gap-3 text-gray-500 hover:text-black">
        <img src="/cart.svg" alt="Cart" />
        <b>1205 руб.</b>
      </li>

      <li class="flex items-center cursor-pointer gap-3 text-gray-500 hover:text-black">
        <img src="/heart.svg" alt="Heart" />
        <span>Закладки</span>
      </li>

      <!-- <li class="flex items-center cursor-pointer gap-3 text-gray-500 hover:text-black">
        <img src="/profile.svg" alt="Profile" />
        <span>Профиль</span>
      </li> -->
    </ul>
  </header>
</template>

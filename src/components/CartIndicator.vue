<template>
  <!-- <router-link> — компонент предназначенный для навигации пользователя в приложении
  с клиентской маршрутизацией. Путь назначения указывается входным параметром to -->
  <router-link
    class="header__cart"
    aria-label="Корзина с товарами"
    :to="{name: 'cart'}"
  >
    <svg
      width="30"
      height="21"
      fill="currentColor"
    >
      <use xlink:href="#icon-cart" />
    </svg>
    <span
      class="header__count"
      aria-label="Количество товаров"
    >
      <!-- C помощью $store получаем доступ к хранилищу (в store/index.js) -->
      {{ $store.state.cartProducts.length }}
    </span>
  </router-link>
</template>

<script>
export default {
};
</script>

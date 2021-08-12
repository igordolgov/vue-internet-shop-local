<template>
  <!-- Шаблон компонента (отдельно от JavaScript) -->
  <li class="catalog__item">
    <!-- <router-link> — компонент предназначенный для навигации пользователя в приложении
    с клиентской маршрутизацией. Путь назначения указывается входным параметром to -->
    <router-link
      class="catalog__pic"
      :to="{name: 'product', params: {id: product.id}}"
    >
      <!-- подключаем картинку товара и с помощью директивы
      v-bind (сокращённо :) связываем её src и alt с товаром -->
      <img
        :src="product.image"
        :alt="product.title"
      >
    </router-link>

    <h3 class="catalog__title">
      <a href="#">
        {{ product.title }} <!-- С помощью интерполяции выводим название товара -->
      </a>
    </h3>

    <span class="catalog__price">
      <!-- С помощью интерполяции выводим цену товара. Используем фильтр (функцию)
      numberFormat для форматирования чисел по разрядам. Выражение слева (product.price)
      будет помещено в эту функцию в качестве первого аргумента -->
      {{ product.price | numberFormat }} &#8381;
    </span>

    <ul class="colors colors--black">
      <li
        class="colors__item"
        v-for="productColors in product.colors"
        :key="productColors.id"
      >
        <label
          class="colors__label"
        >
          <input
            class="colors__radio sr-only"
            type="radio"
            value="productColor.colors"
            v-model="product.colors"
          >
          <span
            class="colors__value"
            :style="{'background-color': productColors,
                     'border': '1px solid grey'}"
          />
        </label>
      </li>
    </ul>
  </li>
</template>

<script>
import gotoPage from '@/helpers/gotoPage';
import numberFormat from '@/helpers/numberFormat';

export default {
  data() {
    return {
      color: '#73B6EA',
    };
  },
  filters: { // ФИЛЬТРЫ (Объект методов). Ключ - название фильтра, значение -
  // функция, которая совершает полезную работу
    numberFormat,
  },
  methods: {
    gotoPage,
  },
  // eslint-disable-next-line vue/require-prop-types
  props: ['product', 'productColor'],
};
</script>

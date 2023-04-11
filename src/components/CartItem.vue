<template>
  <!-- В v-for лучше обращаться не к геттеру, а к вычисляемому свойству -->
  <li
    class="cart__item product"
  >
    <div class="product__pic">
      <img
        :src="item.product.image"
        width="120"
        height="120"
        :alt="item.product.title"
      >
    </div>
    <h3 class="product__title">
      {{ item.product.title }}
    </h3>
    <span class="product__code">
      Артикул: {{ item.product.id }}
    </span>

    <ProductCounter
      class="product__counter form__counter"
      v-model="amount"
      :min-value="1"
    />

    <b class="product__price">
      <!-- Стоимость товаров в корзине: цена товара умноженная на количество -->
      {{ ((item.amount * item.product.price) || '') | numberFormat }} ₽
    </b>

    <button
      class="product__del button-del"
      type="button"
      aria-label="Удалить товар из корзины"
      @click.prevent="deleteProduct(item.productId)"
    >
      <svg
        width="20"
        height="20"
        fill="currentColor"
      >
        <use xlink:href="#icon-close" />
      </svg>
    </button>
  </li>
</template>

<script>
// eslint-disable-next-line import/no-unresolved
import numberFormat from '@/helpers/numberFormat'; // Форматирование цены
import { mapMutations } from 'vuex';
// eslint-disable-next-line import/no-unresolved
import ProductCounter from '@/components/ProductCounter.vue';

export default {
  components: { ProductCounter },
  filters: { numberFormat }, // Форматирование цены (подключаем как фильтр)
  // eslint-disable-next-line vue/require-prop-types
  props: ['item'],
  computed: {
    amount: {
      get() {
        return this.item.amount;
      },
      set(value) {
        this.$store.commit('updateCartProductAmount', { productId: this.item.productId, amount: value });
      },
    },
  },
  methods: {
    ...mapMutations({ deleteProduct: 'deleteCartProduct' }),
  },
};
</script>

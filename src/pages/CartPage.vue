<!-- eslint-disable vue/no-deprecated-filter -->
<template>
<main class="content container">
    <div class="content__top">
      <ul class="breadcrumbs">
        <li class="breadcrumbs__item">
          <a class="breadcrumbs__link" href="index.html">
            Каталог
          </a>
        </li>
        <li class="breadcrumbs__item">
          <a class="breadcrumbs__link">
            Корзина
          </a>
        </li>
      </ul>

      <h1 class="content__title">
        Корзина
      </h1>
      <span class="content__info">
        {{ $store.state.cartProducts.length }} товара
      </span>
    </div>
    <div v-if="isLoadingCart" class="cart-loading">
      <img src="/img/logspiner.gif" alt="Loading..." />
      Загруска товаров в корзине...
    </div>
<div v-else-if="hasFailedLoadingCart" class="cart-loading">
  Произошла ошибка при загруске товаров, нет соеединения с сервером.Попробовать еще раз
  </div>
<div v-else>
    <section class="cart">
      <form class="cart__form form" action="#" method="POST">
        <div class="cart__field">
          <ul class="cart__list">
            <CartItem v-for="item in products" :key="item.productId" :item="item"/>
          </ul>
        </div>

        <div class="cart__block">
          <p class="cart__desc">
            Мы&nbsp;посчитаем стоимость доставки на&nbsp;следующем этапе
          </p>
          <p class="cart__price">
            Итого: <span>{{ totalPrice | numberFormat}} $</span>
          </p>

          <router-link _tag:button :to="{name: 'order'}" class="cart__button button button--primery" type="submit">
            Оформить заказ
          </router-link>
        </div>
      </form>
    </section>
  </div>
  </main>
</template>

<script>
import numberFormat from '@/helpers/numberFormat';
import { mapGetters } from 'vuex';
import CartItem from '@/components/CartItem.vue';
export default {
  filters: {numberFormat},
  components: {CartItem},
  computed: {
    ...mapGetters({products: 'cartDetailProducts', totalPrice: 'cartTotalPrice'}),
    isLoadingCart(){
      return this.$store.state.isLoadingCart;
    },
    hasFailedLoadingCart(){
      return this.$store.state.hasFailedLoadingCart;
    }
  },
  mounted() {
    this.$store.dispatch('loadCart');
  },
}
</script>

<style>
.cart-loading {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 200px;
  font-size: 24px;
  color: #999;
}
</style>
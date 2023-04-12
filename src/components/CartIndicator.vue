<template>
 <router-link class="header__cart" aria-label="Корзина с товарами" :to="{name: 'cart'}" >
          <svg width="30" height="21" fill="currentColor">
            <use xlink:href="#icon-cart"></use>
          </svg>
          <span v-if="isLoadingCart" class="header__count" aria-label="Количество товаров">
            <img src="/img/logspiner.gif" alt="Loading..." style="height: 15px;"/>
            </span>
          <span v-else-if="hasFailedLoadingCart">Произошла ошибка при загруске товаров.Попробовать еще раз</span>
          <span v-else class="header__count" aria-label="Количество товаров">{{ $store.state.cartProducts.length }}</span>
        </router-link>
</template>

<script>

export default {
  computed:{
    isLoadingCart(){
      return this.$store.state.isLoadingCart;
    },
    hasFailedLoadingCart(){
      return this.$store.state.hasFailedLoadingCart;
    }
  }
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
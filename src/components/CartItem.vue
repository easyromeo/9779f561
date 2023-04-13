<!-- eslint-disable vue/no-deprecated-filter -->
<template>
<li class="cart__item product">
              <div class="product__pic">
                <img :src="item.product.image" width="120" height="120" :alt="item.product.title">
              </div>
              <h3 class="product__title">
                {{ item.product.title }}
              </h3>
              <span class="product__code">
                Артикул: {{ item.product.id }}
              </span>

              <div class="product__counter form__counter">
                 <addAmount :value="amount" @quantity-changed="amount = $event" class="adamount"/>
              </div>

              <b class="product__price">
                {{ (item.amount * item.product.price) | numberFormat }} $
              </b>

              <button class="product__del button-del" type="button" aria-label="Удалить товар из корзины" @click.prevent="removeProduct(item.productId)">
                <svg width="20" height="20" fill="currentColor">
                  <use xlink:href="#icon-close"></use>
                </svg>
              </button>
            </li>
</template>

<script>
import numberFormat from '@/helpers/numberFormat';
import addAmount from '@/components/addAmount.vue';

export default {
  components:{addAmount},
    filters: {numberFormat},
    props:['item'],
    computed: {
        amount: {
            get(){
                return this.item.amount;
            },
            set(value){
                this.$store.dispatch('updateCartProductAmount', {productId: this.item.productId, amount: value});
            }
        }
    },
    methods: {
        removeProduct(productId) {
            this.$store.dispatch('removeCartProduct', productId);
        },
    }
}
</script>

<style>
.adamount{
  height: auto;width: 105px;
}
</style>
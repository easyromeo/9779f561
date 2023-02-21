<template>
  <ul class="catalog__list">
      <ProductItem v-for="products in products" :key="products.id" :products="products"></ProductItem>
  </ul>
</template>

<script>
import ProductItem from './ProductItem.vue';

export default {
  components: { ProductItem },
  props: ['products']
};

</script>

<template>
  <ProductList :product="products" />
</template>

<script>
import ProductList from './components/ProductList.vue';
import products from './data/products';

export default {
  name: 'App',
  components: { ProductList },
  data() {
    return {
      products,
    };
  },
};
</script>

<style lang="stylus">

</style>

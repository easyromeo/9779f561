<!-- eslint-disable vue/no-deprecated-v-bind-sync -->
<template>
  <main class="content container">
    <div class="content__top content__top--catalog">
      <h1 class="content__title">
        Каталог
      </h1>
      <span class="content__info">
        152 товара
      </span>
    </div>
    <div class="content__catalog">
      <ProductFilter :price-from.sync="filterPriceFrom" :price-to.sync="filterPriceTo" :category-id.sync="filterCategoryId" :colorId.sync="filterColor" />

      <section class="catalog">

        <div v-if="productsLoading" class="cart-loading"><img src="/img/logspiner.gif" alt="loading"> Загруска товаров...</div>
        <div v-if="productsLoadingFailed" class="cart-loading">Произошла ошибка при загруске товаров <button @click.prevent="loadProducts">Попробовать еще раз</button></div>

        <ProductList :products="products"/>

        <BasePagination v-model="page" :count="countProducts" :per-page="productsPerPage" />
      </section>

    </div>
</main>
</template>
<script>
import ProductList from '@/components/ProductList.vue';
import BasePagination from '@/components/BasePagination.vue';
import ProductFilter from '@/components/ProductFilter.vue';
import axios from 'axios';
import { API_BASE_URL } from '@/config';

export default {
  components: { ProductList, BasePagination, ProductFilter },
  data() {
    return {
      filterPriceFrom: 0,
      filterPriceTo: 0,
      filterCategoryId: 0,
      filterColor: 0,

      page: 1,
      productsPerPage: 3,

      productsData: null,

      productsLoading: false,
      productsLoadingFailed: false
    }
  },
  computed: {
      products() {
      return this.productsData 
      ? this.productsData.items.map(product => {
        return {
          ...product,
          image: product.image.file.url
        }
      })
      : [];
    },
    countProducts() {
      return this.productsData ? this.productsData.pagination.total : 0;
    },
  },
  methods:{
    loadProducts(){
      this.productsLoading = true;
      this.productsLoadingFailed = false;
      clearTimeout(this.loadProductsTimer);
      this.loadProductsTimer = setTimeout(() => {
        axios.get(API_BASE_URL + `/api/products`, {
        params: {
          page: this.page,
          limit: this.productsPerPage,           
          minPrice: this.filterPriceFrom,
          maxPrice: this.filterPriceTo,
          categoryId: this.filterCategoryId,
          colorId: this.filterColor
        }
       })
       .then(response => this.productsData = response.data)
       .catch(() => this.productsLoadingFailed = true)
       .then(() => this.productsLoading = false);
      }, 500);

    }
  },
  watch: {
    page(){
      this.loadProducts();
    },
    filterPriceFrom(){
      this.loadProducts();
    },
    filterPriceTo(){
      this.loadProducts();
    },
    filterCategoryId(){
      this.loadProducts();
    },
    filterColor(){
      this.loadProducts();
    },
  },
  created(){
    this.loadProducts();
  }
};
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

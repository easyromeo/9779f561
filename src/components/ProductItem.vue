<!-- eslint-disable vue/no-deprecated-filter -->
<template>
    <li class="catalog__item">
        <router-link class="catalog__pic" href="#" :to="{name: 'product', params: {id: products.id}}">
                <img :src="products.image" :alt="products.title">
            </router-link>

            <h3 class="catalog__title">
                <a href="#">
                    {{ products.title }}
                </a>
            </h3>

            <span class="catalog__price">
                {{ products.price | numberFormat }} $
            </span>

            <ul class="colors colors--black">
                <li class="colors__item" v-for="color in products.colors" :key="color.id">
                    <label class="colors__label">
                        <input class="colors__radio sr-only" type="radio" :value="color.color">
                        <span class="colors__value" :style="{ backgroundColor: color.color }">
                        </span>
                    </label>
                </li>
            </ul>
    </li>
</template>

<script>
import gotoPage from "@/helpers/gotoPage";
import numberFormat from "@/helpers/numberFormat";

export default {
    filters: {
        numberFormat
    },
    methods: {
        gotoPage
    },
  props: ['products'],
};

</script>

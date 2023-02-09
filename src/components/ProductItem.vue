<!-- eslint-disable max-len -->
<!-- eslint-disable vuejs-accessibility/label-has-for -->
<template>
    <section class="catalog">

        <span :product="products">
            <a class="catalog__pic" href="#">
                <img :src="products.image" :alt="products.title">
            </a>

            <h3 class="catalog__title">
                <a href="#">
                    {{ products.title }}
                </a>
            </h3>

            <span class="catalog__price">
                {{ products.price + '$' }}
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
        </span>
    </section>
</template>

<script>
export default {
  props: ['products'],
};

</script>

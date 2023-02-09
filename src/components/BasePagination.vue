<!-- eslint-disable max-len -->
<template>
  <ul class="catalog__pagination pagination">
    <li class="pagination__item">
      <a href="#" class="pagination__link pagination__link--arrow " aria-label="Предыдущая страница"
       :class="{ 'pagination__link--disabled': page == 1 }" @click.prevent="prevPage()">
        <svg width="8" height="14" fill="currentColor">
          <use xlink:href="#icon-arrow-left"></use>
        </svg>
      </a>
    </li>
    <li class="pagination__item" v-for="page in pages" :key="page">
      <a href="#" class="pagination__link" :class="{ 'pagination__link--current': page === pages }"
        @click.prevent="paginate(page)">
        {{ page }}
      </a>
    </li>
    <li class="pagination__item">
      <a href="#" class="pagination__link pagination__link--arrow" aria-label="Следующая страница"
        :class="{ 'pagination__link--disabled': page === pages }" @click.prevent="nextPage(page)">
        <svg width="8" height="14" fill="currentColor">
          <use xlink:href="#icon-arrow-right"></use>
        </svg>
      </a>
    </li>
  </ul>
</template>

<script>
export default {
  model: {
    prop: 'page',
    event: 'paginate',
  },
  props: ['page', 'count', 'perPage'],
  computed: {
    pages() {
      return Math.ceil(this.count / this.perPage);
    },
  },
  methods: {
    paginate(page) {
      this.$emit('paginate', page);
    },
    nextPage(page) {
      if (page < this.pages) { this.$emit('paginate', page + 1); }
    },
    prevPage() {
      if (this.page <= 1) {
        this.$emit('paginate', this.page);
      } else {
        this.paginate(this.page - 1);
      }
    },
  },
};

</script>

<template> 
 <div class="form__counter">      
    <button type="button" aria-label="Убрать один товар" @click="decrement">
        <svg width="12" height="12" fill="currentColor">
        <use xlink:href="#icon-minus"></use>
        </svg>
    </button>

    <input type="text" v-model.number="quantity">

    <button type="button" aria-label="Добавить один товар" @click="increment">
        <svg width="12" height="12" fill="currentColor">
        <use xlink:href="#icon-plus"></use>
        </svg>
    </button>
</div>              
</template>

<script>
export default {
  props: {
    value: {
      default: 1
    },
  },
  data() {
    return {
      quantity: this.value,
    };
  },
  methods: {
    decrement() {
      if (this.quantity > 1) {
        this.quantity -= 1;
        this.$emit('quantity-changed', this.quantity);
      }
    },
    increment() {
      this.quantity += 1;
      this.$emit('quantity-changed', this.quantity);
    }
  },
};
</script>
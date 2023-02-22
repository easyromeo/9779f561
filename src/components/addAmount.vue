<template> 
 <div class="form__counter">      
    <button type="button" aria-label="Убрать один товар" @click.prevent="minusAmount()">
        <svg width="12" height="12" fill="currentColor">
        <use xlink:href="#icon-minus"></use>
        </svg>
    </button>

    <input type="text" v-model.number="productAmount">

    <button type="button" aria-label="Добавить один товар" @click.prevent="plusAmount()">
        <svg width="12" height="12" fill="currentColor">
        <use xlink:href="#icon-plus"></use>
        </svg>
    </button>
</div>              
</template>

<script>
export default {
 data(){
    return {
      productAmount: 1
    };
  },
 methods:{
    plusAmount(){
        this.productAmount = this.productAmount + 1
      },
    minusAmount(){
        if(this.productAmount <= 1){
            this.productAmount = 1
        }else{
            this.productAmount = this.productAmount - 1
        }
        
      }
    }
}
</script>
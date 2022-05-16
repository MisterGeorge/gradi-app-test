<script setup>
  import { ref, computed } from 'vue'

  // Components
  import GButton from './GButton.vue'
  import GInput from './GInput.vue'

  defineProps({
    price: {
      type: Number,
      required: true,
      default: 0
    }
  })

  const quantity = ref(0)

  const increment = () => {
    quantity.value++
  }

  const decrement = () => {
    if ( quantity.value > 0 ) {
      return quantity.value--
    }

    return quantity.value = 0   
  }

  const triggerEvent = (event) => {
    this.$emit('input', event.target.value);
  }

  const totalPriceComputed = computed(() => {
    if (quantity.value === 0) return price;
    return quantity.value > 0 ? `${quantity.value * price}` : `${price}`;
  });
</script>

<template>
  <div class="product-quantity">
    <div class="btn-groups">
      <GButton
        label="-"
        name="btn-minus"
        type="button"
        :disabled=false
        :autofocus=false
        classCustom="bg-default btn-small form-input-quantity"
        @click="decrement"
      />
      <GInput
        type="text"
        name="quantity"
        placeholder="0"
        required="required"
        disabled=false
        autofocus=false
        autocomplete="off"
        :value="quantity"
        @input="triggerEvent"
      />
      <GButton
        label="+"
        name="btn-plus"
        type="button"
        :disabled=false
        classCustom="bg-default btn-small form-input-quantity"
        @click="increment"
      />
    </div>
    <div class="total-price">
      <span class="title">Total price:</span>
      <span class="price"> $ {{ price }}</span>
    </div>
  </div>
</template>

<style lang="scss" scoped>
  @import '../mixins';
  @import '../colors';

  .btn-small {
    width: 3em;
    height: 3em;
    @include padding(0, 0, 0, 0);
    @include margin(0, .2em, 0, .2em);
  }
  
  .product-quantity {
    @include flexbox;
    @include justify-content(space-between);
    overflow: hidden;
    @include padding(1rem, 0, 1rem, 0);
    @include border(bottom, thin, solid, $gray-300);

    .btn-groups {
      @include flexbox;
      @include flex-wrap(wrap);
      @include justify-content(center);
      @include align-items(center);
      @include padding(0, 0, 0, 0);
      @include margin(0, 0, 0, 0);
      @include border('', thin, solid, $gray-300);

      .form-input {
        width: 3em;
        height: 3em;
        @include margin(0, 0, 0, 0);
        background-color: $bg-transparent;
        @include border('', thin, solid, $bg-transparent);
      }

      .form-input-quantity {
        @include padding(0, 0, 0, 0);
        @include margin(0, 0, 0, 0);
        background-color: $bg-transparent;
        @include border('', thin, solid, $bg-transparent);
      }
    }

    .total-price {
      color: $gray-600;
      font-weight: 400;
      font-size: .875rem;
      text-transform: none;
      letter-spacing: 0;
      font-family: Avenir, Helvetica, Arial, sans-serif;
      @include align-self(center);

      .price {
        color: $gray-800;
        font-weight: 800;
      }
    }
  }
</style>
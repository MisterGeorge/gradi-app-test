<script setup>
  defineProps({
    title: {
      type: String,
      required: true
    },
    sizes: {
      type: Array,
      required: true
    }
  })
</script>

<template>
  <div class="product-sku">
    <span class="sku-title">{{ title }}</span>
    <ul class="sku-list">
      <li
        v-for="(size, i) in sizes"
        :key="i"
        class="sku-item"
      >
        <a href="#">{{ size }}</a>
      </li>
    </ul>
  </div>
</template>

<style lang="scss" scoped>
  @import '../mixins';
  @import '../colors';

  .product-sku {
    @include flexbox;
    overflow: hidden;
    @include padding(1rem, 0, 1rem, 0);
    @include border(bottom, thin, solid, $gray-300);

    .sku-title {
      color: $gray-600;
      font-weight: 400;
      font-size: .875rem;
      text-transform: none;
      letter-spacing: 0;
      font-family: Avenir, Helvetica, Arial, sans-serif;
      @include align-self(center);
    }

    .sku-list {
      @include flexbox;
      @include flex-wrap(wrap);
      @include justify-content(flex-start);
      @include align-items(flex-start);
      @include margin(0, 0, 0, 0);
      list-style: none;

      .sku-item {
        width: 40px;
        height: 40px;
        @include flexbox;
        @include align-items(center);
        @include padding(0, 0, 0, 0);
        @include margin(0, .2em, 0, .2em);

        a {
          width: 40px;
          height: 40px;
          text-decoration: none;
          color: $gray-600;
          font-family: Avenir, Helvetica, Arial, sans-serif;
          @include border-radius (0);
          @include border('', thin, solid, $gray-600);
          @include padding(0, 0, 0, 0);
          @include flexbox;
          @include flex-wrap(wrap);
          @include justify-content(center);
          @include align-items(center);

          &:hover { 
            color: $gray-900 ;
            @include border('', thin, solid, $gray-900);
          }
        }
      }
    }
  }

  /* Small only */
  @media screen and (max-width: 39.9375em) {
    .product-sku {

      .sku-list {
        .sku-item {
          @include margin(0, .2em, .2em, .2em);
        }
      }
    }
  }
</style>
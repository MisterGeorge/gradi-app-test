<script setup>
  defineProps({
    title: {
      type: String,
      required: true
    },
    colors: {
      type: Array,
      required: true
    },
    classCustom: {
      type: String,
      required: true
    }
  })

  const getColorSku = (str) => {
    let ctx = document.createElement("canvas").getContext("2d");
    ctx.fillStyle = str;
    return ctx.fillStyle;
  }
</script>

<template>
  <div class="product-sku">
    <span class="sku-title">{{ title }}</span>
    <ul class="sku-list">
      <li
        v-for="(color, i) in colors"
        :key="i"
        class="sku-item"
      >
        <a href="#" :style="`background-color: ` + `${getColorSku(color)}` + `; border: thin solid ` + `${getColorSku(color)}`"></a>
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
        width: 1.5em;
        height: 1.2em;
        @include flexbox;
        @include align-items(center);
        @include padding(0, 0, 0, 0);
        @include margin(0, .2em, 0, .2em);

        a {
          width: 1.5em;
          height: 1.5em;
          text-decoration: none;
          color: $gray-600;
          font-family: Avenir, Helvetica, Arial, sans-serif;
          @include border-radius (100%);
          @include border('', thin, solid, trasnparent);
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
</style>
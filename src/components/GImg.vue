<script setup>
  defineProps({
    src: {
      type: String,
      required: true
    },
    alt: {
      type: String,
      required: true
    },
    width: {
      type: Number,
      required: true
    },
    height: {
      type: Number,
      required: true
    }
  })
</script>

<template>
  <figure>
    <img
      class="image__auto"
      :src="src"
      :alt="alt"
      :width="width"
      :height="height"
    >
  </figure>
</template>

<style lang="scss" scoped>
  @import '../mixins';
  @import '../colors';

  figure {
    @include flexbox;
    @include flex-wrap(wrap);
    @include justify-content(center);
    @include align-items(center);
    @include margin(0, .5rem, 0, .5rem);
    background-color: $bg-image;

      .image__auto {
        max-width: 100%;
        height: auto;
      }
  }
</style>
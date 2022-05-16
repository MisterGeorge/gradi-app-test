<script setup lang="ts">
  defineProps({
    crumbs: {
      type: Array,
      required: true,
    }
  })
</script>

<template>
  <nav class="breadcrumb" aria-label="breadcrumbs">
    <ul class="breadcrumb-list">
      <li
        v-for="(link, item) in crumbs"
        :key="item"
        class="breadcrumb-item"
      >
        <a href="#">{{ link }}</a>
      </li>
    </ul>
  </nav>
</template>

<style lang="scss" scoped>
  @import '../mixins';
  @import '../colors';

  .breadcrumb {
    user-select: none;
    font-size: 1rem;
    white-space: nowrap;
    display: block;

    .breadcrumb-list {
      @include flexbox;
      @include flex-wrap(wrap);
      @include justify-content(flex-start);
      @include align-items(flex-start);
      list-style: none;
      @include padding(null, null, null, .5rem);

      .breadcrumb-item {
        @include flexbox;
        @include align-items(center);

        &:first-child::before { content: "" }

        &::before {
          color: $gray-600;
          content: "/";
        }

        a {
          @include padding(0, .75em, 0, .75em);
          text-decoration: none;
          color: $gray-600;
          font-family: Avenir, Helvetica, Arial, sans-serif;

          &:hover { color: $gray-900 }
        }
      }
    }
  }
</style>
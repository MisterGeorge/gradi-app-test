<script setup>
  import GBreadcrumb from './components/GBreadcrumb.vue'
  import GProduct from './components/GProduct.vue'

  const crumbs = ['Cataglog','Sneackers', 'Free Trainer 3', 'MMW'];
</script>

<template>
  <div class="container">
    <div class="row">
      <div class="col">
        <GBreadcrumb :crumbs="crumbs" />
      </div>
    </div>
    
    <GProduct />
  </div>
</template>

<style lang="scss" scoped>
  @import 'mixins';
  @import 'colors';

  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    @include margin(3.75rem, null, null, null);
  }
</style>

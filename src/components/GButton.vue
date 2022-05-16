<script setup>
  defineProps({
    label: {
      type: String,
      required: true
    },
    name: {
      type: String,
      required: true
    },
    type: {
      type: String,
      required: true
    },
    disabled: {
      type: Boolean,
      required: true
    },
    autofocus: {
      type: Boolean,
      required: true
    },
    classCustom: {
      type: String,
      required: false
    }
  })
</script>

<template>
  <button
    :name="name"
    :type="type"
    :disabled="disabled"
    :autofocus="autofocus"
    :class="classCustom"
    class="btn"
  >
    {{ label }}
  </button>
</template>

<style lang="scss" scoped>
  @import '../mixins';
  @import '../colors';

  .btn {
    @include flexbox;
    @include justify-content(center);
    @include align-items(center);
    width: 100%;
    font-weight: 400;
    line-height: 1.5;
    color: $gray-900;
    text-decoration: none;
    cursor: pointer;
    -webkit-user-select: none;
    -moz-user-select: none;
    user-select: none;
    background-color: transparent;
    @include border-radius (.25rem);
    @include border('', thin, solid, trasnparent);
    @include padding(.375rem, .75rem, .375rem, .75rem);
    transition: color .15s ease-in-out,background-color .15s ease-in-out,border-color .15s 
  }
</style>
<script setup>
  defineProps({
    type: {
      type: String,
      required: true
    },
    name: {
      type: String,
      required: true
    },
    placeholder: {
      type: String,
      required: true
    },
    required: {
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
    autocomplete: {
      type: String,
      required: true
    },
    classCustom: {
      type: String,
      required: false
    }
  })
</script>

<template>
  <input
    :type="type"
    :name="name"
    :placeholder="placeholder"
    :required="required"
    :disabled="disabled"
    :autofocus="autofocus"
    :autocomplete="autocomplete"
    :class="classCustom"
    class="form-input"
    @input="$emit($event.target.name, $event.target.value)"
  >
</template>

<style lang="scss" scoped>
  @import '../mixins';
  @import '../colors';

  .form-input {
    width: auto;
    font-size: 1rem;
    font-weight: 400;
    line-height: 1.5;
    color: $gray-800;
    background-clip: padding-box;
    -webkit-appearance: none;
       -moz-appearance: none;
            appearance: none;
    @include border-radius (.25rem);
    @include border('', thin, solid, $gray-300);
    @include padding(.375rem, .75rem, .375rem, .75rem);
  }
</style>
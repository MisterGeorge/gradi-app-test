<script>
  // Components

  export default {
    name: 'GModal',
    component: [],
    methods: {
      close() {
        this.$emit('close');
      }
    },
  };
</script>

<template>
  <transition name="modal-fade">
    <div class="modal-backdrop">
      <div class="modal"
        role="dialog"
        aria-labelledby="modalTitle"
        aria-describedby="modalDescription"
      >
        <header class="modal-header" id="modalTitle">
          <slot name="header">
            This is the default title!
          </slot>
          <button 
            type="button" 
            class="btn btn-close bg-black" 
            @click="close"
          >x</button>
        </header>

        <section class="modal-body" id="modalDescription">
          <slot name="body">
            This is the default body!
          </slot>
        </section>

        <footer class="modal-footer">
          <slot name="footer">
            This is the default footer!
          </slot>
        </footer>
      </div>
    </div>
  </transition>
</template>

<style lang="scss" scoped>
  @import '../mixins';
  @import '../colors';

  .modal-backdrop {
    position: fixed;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    @include flexbox;
    @include justify-content(center);
    @include align-items(center);
    background-color: rgba($black, 0.3);

    .modal {
      width: 100%;
      max-width: 31.25rem;
      background: $white;
      box-shadow: 0 0.5rem 1rem rgba($black, 0.15);
      overflow-x: auto;
      @include flexbox;
      @include flex-direction(column);

      .modal-header,
      .modal-body,
      .modal-footer {
        text-transform: none;
        letter-spacing: 0;
        font-family: Avenir, Helvetica, Arial, sans-serif;
        @include flexbox;
        @include padding(1.125rem, 1.125rem, 1.125rem, 1.125rem);
      }

      .modal-header {
        position: relative;
        color: $gray-700;
        font-weight: 600;
        font-size: 1.2rem;
        @include justify-content(space-between);
        @include border(bottom, thin, solid, $gray-200);

        .btn-close {
          position: absolute;
          top: .5em;
          right: .5em;
          font-size: 20px;
          cursor: pointer;
          font-weight: bold;
          @include border('', thin, solid, transparent);
          @include padding(.3rem, .6rem, .3rem, .6rem);
        }
      }

      .modal-body,
      .modal-footer {
        color: $gray-600;
        font-weight: 400;
        font-size: 1rem;
      }

      .modal-body {
        position: relative;
        @include padding(1.125rem, 1.125rem, 1.125rem, 1.125rem);
      }

      .modal-footer {
        @include flexbox;
        @include justify-content(center);
        @include border(top, thin, solid, $gray-200);
      }
    }
  }

  .modal-fade-enter,
  .modal-fade-leave-to {
    @include opacity(0);
  }

  .modal-fade-enter-active,
  .modal-fade-leave-active {
    @include transition(opacity, .5s, ease);
  }

  .btn-large {
    font-size: 1.25rem;
    @include padding(.5rem, 1rem, .5rem, 1rem);
  }

  .bg-black {
    color: $white;
    background-color: $bg-black;
    @include border-radius (0);
    @include border('', thin, solid, $bg-black);
  }

  .bg-default {
    background-color: $bg-light;
    @include border-radius (0);
    @include border('', thin, solid, $bg-light);
  }

  /* Small only */
  @media screen and (max-width: 39.9375em) {
    .modal-backdrop {
       .modal {
         width: 95%;
         @include margin(0, auto, 0, auto);
       }
    }
  }
</style>
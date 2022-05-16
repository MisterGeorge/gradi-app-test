<script setup>
  import { ref, onMounted, reactive } from 'vue'
  import { VueperSlides, VueperSlide } from 'vueperslides'
  import 'vueperslides/dist/vueperslides.css'

  // Components
  import GImg from './GImg.vue'
  import GSkuSize from './GSku-sizes.vue'
  import GSkuColor from './GSku-colors.vue'
  import GProductQuantity from './GProduct-quantity.vue'
  import GButton from './GButton.vue'
  import GModal from './GModal.vue'

  const product  = ref({})
  const images   = ref([])
  const colors   = ref([])
  const sizes    = ref([])
  const thumbs   = ref([])
  const variants = ref([])
  const isModalVisible = ref(false)

  onMounted(async () => {
    const response = await fetch("https://graditest-store.myshopify.com/products/free-trainer-3-mmw.js");
    const data  = await response.json();

    product.value  = data
    images.value   = data.images
    colors.value   = data.options[0]
    sizes.value    = data.options[1]
    thumbs.value   = data.media
    variants.value = data.variants
  });

  const showModal = () => {
    isModalVisible.value = true
  }

  const closeModal = () => {
    isModalVisible.value = false
  }
</script>

<template>
  <div class="row">
    <div class="col">
      <div class="row">
        <div class="col">
          <GImg
            :src="product.featured_image" 
            :alt="product.title"
            :width="399"
            :height="399"
          />
        </div>
      </div>
      <div class="row" v-if="thumbs.length">
          <div class="col" v-for="media in thumbs" :key="media.id">
            <GImg 
              :src="media.src"
              :alt="media.alt"
              :width="media.width"
              :height="media.height"
            />
          </div>
      </div>
    </div>
    <div class="col">
      <span class="product-brand">by Nike x ALYX</span>
      <h1 class="product-name">{{ product.title }}</h1>
      <div class="product-price">
        <span class="selling-price">$ {{ product.price }}</span>
        <span class="list-price">$ {{ product.compare_at_price_max }}</span>
      </div>

      <GSkuColor :title="colors.name" :colors="colors.values" />

      <GSkuSize :title="sizes.name" :sizes="sizes.values" />

      <GProductQuantity :price="product.price" />

      <div class="product-buttons">
        <GButton
          label="Add to favorite"
          name="add-to-favorite"
          type="button"
          :disabled=false
          :autofocus=false
          classCustom="bg-default btn-large"
        />
        <GButton
          label="Add to cart"
          name="add-to-cart"
          type="button"
          :disabled=false
          :autofocus=false
          classCustom="bg-black btn-large"
          @click="showModal"
        />
      </div>

      <div class="product-description" v-html="product.description"></div>
    </div>

    <GModal v-show="isModalVisible" @close="closeModal">
      <template v-slot:header>
        Add to cart
      </template>

      <template v-slot:body>
        <div>
          <select class="form-select">
            <option v-for="variant in variants" :value="variant" :key="variant">
              {{ variant.name }}
            </option>
          </select>
        </div>
      </template>

      <template v-slot:footer>
        <GButton
          label="Add to cart"
          name="add-to-cart"
          type="button"
          :disabled=false
          :autofocus=false
          classCustom="bg-default"
        />
        <GButton
          label="Cerrar"
          name="close"
          type="button"
          :disabled=false
          :autofocus=false
          classCustom="bg-black"
          @click="closeModal"
        />
      </template>
    </GModal>
  </div>
</template>

<style lang="scss" scoped>
  @import '../mixins';
  @import '../colors';

  .product-brand {
    color: $gray-600;
    font-family: Avenir, Helvetica, Arial, sans-serif;
    font-weight: 400;
    text-transform: none;
    letter-spacing: 0;
  }

  .product-name {
    font-size: 24px;
    font-weight: 600;
    color: $gray-800;
    line-height: normal;
    text-transform: capitalize;
    font-family: Avenir, Helvetica, Arial, sans-serif;
  }

  .product-price {
    @include padding(null, null, 2rem, null);
    @include border(bottom, thin, solid, $gray-300);

    .selling-price {
      font-size: 24px;
      font-weight: 600;
      color: $gray-800;
      line-height: normal;
      font-family: Avenir, Helvetica, Arial, sans-serif;
      @include margin(null, 1.5rem, null, null);
    }

    .list-price {
      font-size: 15px;
      font-weight: 400;
      color: $gray-600;
      text-transform: none;
      letter-spacing: 0;
      line-height: normal;
      font-family: Avenir, Helvetica, Arial, sans-serif;
      text-decoration: line-through;
    }
  }

  .product-buttons {
    @include flexbox;
    width: 100%;
    @include margin(2rem, 0, 2rem, 0);

    .btn {
      width: 50%;
    }
  }

  .product-description {
    span {
      font-size: 14px;
      font-weight: 400;
      color: $gray-800;
      line-height: normal;
      text-transform: capitalize;
      font-family: Avenir, Helvetica, Arial, sans-serif;
    }
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
</style>
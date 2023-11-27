<template>
  <div class="card flex">
    <!-- Available product -->
    <div class="card__img__product">
      <img :src="product.image" alt="product" />
    </div>
    <div class="card__body">
      <h3
        class="title__product"
        :class="
          product.category === 'men\'s clothing' ? 'color__men' : 'color__women'
        "
      >
        {{ product.title }}
      </h3>
      <div class="category__product">
        <span class="category__product">{{ product.category }}</span>
        <div class="rating__product">
          <span class="rating__product__text">{{ product.rating.rate }}/5</span>
          <span class="rating__product__star">⚫⚫⚫⚪⚪</span>
        </div>
      </div>
      <hr />
      <p class="description__product">
        {{ truncateDescription(150) }}
      </p>
      <div class="card__footer">
        <hr />
        <div class="price__product">
          <span
            class="price__product__number"
            :class="
              product.category === 'men\'s clothing'
                ? 'color__men'
                : 'color__women'
            "
            >${{ product.price }}</span
          >
        </div>
        <div class="button__product">
          <button
            class="button button__buy button__color"
            :class="
              product.category === 'men\'s clothing'
                ? 'button__men__color'
                : 'button__women__color'
            "
          >
            Buy now
          </button>
          <button
            class="button button__next"
            :class="
              product.category === 'men\'s clothing'
                ? 'color__men button__men__color'
                : 'color__women button__women__color'
            "
            @click="$emit('next-product', product)"
          >
            Next product
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import "../assets/style/custom.css";

export default {
  name: "ProductDisplay",
  props: ["product", "showNextProduct", "ProductAvailable"],
  methods: {
    truncateDescription(limit) {
      return this.product.description.length > limit
        ? `${this.product.description.substring(0, limit)}...`
        : `${this.product.description}`;
    },
  },
};
</script>

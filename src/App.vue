<template>
  <div id="app">
    <div
      :class="
        !ProductAvailable
          ? 'bg__unavailable__color'
          : currentProduct.category === 'men\'s clothing'
          ? 'bg__color__men'
          : 'bg__color__women'
      "
      class="container flex justify__center items__center"
    >
      <ProductDisplay
        v-if="ProductAvailable"
        :product="currentProduct"
        @next-product="showNextProduct"
      />
      <UnavailableProduct
        v-else
        :product="currentProduct"
        :ProductAvailable="ProductAvailable"
        @next-product="showNextProduct"
      />
    </div>
  </div>
</template>

<script>
import ProductDisplay from "./components/ProductDisplay.vue";
import UnavailableProduct from "./components/UnavailableProduct.vue";
import "../src/assets/style/custom.css";
import axios from "axios";

export default {
  name: "App",
  components: {
    ProductDisplay,
    UnavailableProduct,
  },
  props: [],

  data() {
    return {
      products: [],
      currentProduct: {}, // Produk yang sedang ditampilkan
      currentIndex: 0, // Indeks produk yang sedang ditampilkan
      ProductAvailable: false,
    };
  },
  methods: {
    setProduct(data) {
      this.products = data;
      // Menampilkan produk pertama
      this.currentProduct = this.products[this.currentIndex];
      this.setAvailability();
    },
    showNextProduct() {
      // Kembali ke index awal jika sudah mencapai batas index
      this.currentIndex = (this.currentIndex + 1) % this.products.length;
      // Menampilkan produk berikutnya
      this.currentProduct = this.products[this.currentIndex];
      this.setAvailability();
    },
    setAvailability() {
      const product = this.currentProduct;
      if (
        product.category === "men's clothing" ||
        product.category === "women's clothing"
      ) {
        this.ProductAvailable = true;
      } else {
        this.ProductAvailable = false;
      }
    },
  },
  mounted() {
    axios
      .get(`https://fakestoreapi.com/products`)
      .then((response) => {
        this.setProduct(response.data);
      })
      .catch((error) => {
        console.log(error);
      });
  },
};
</script>

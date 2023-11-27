<template>
  <!-- Unavailable product -->
  <div
    class="card-unavailable"
    :class="!ProductAvailable ? 'display-none' : 'display-yes'"
  >
    <div class="row-unavailable">
      <h2 class="unavailable-message">This product is unavailable to show</h2>
      <button class="btn-unavailable" @click="$emit('next-product', product)">
        Next Product
      </button>
    </div>
  </div>
</template>

<script>
import "../assets/style/custom.css";

export default {
  name: "UnavailableProduct",
  props: ["product", "ProductAvailable"],
};
</script>

<script setup>
import { ref } from "vue";
import greenSock from "../assets/images/socks_green.jpg";
import blueSock from "../assets/images/socks_blue.jpg";
import ProductInfo from "./ProductInfo.vue";
const products = ref({
  product: "Socks",
  image: greenSock,
  stock: 100,
  details: ["50% cotton", "30% wool", "20% polyester"],
  variants: [
    { id: 1, color: "green", image: greenSock },
    { id: 2, color: "blue", image: blueSock },
  ],
  updateImage: function (variantImage) {
    this.image = variantImage;
  },
});
</script>
<template>
  <main class="container">
    <div class="row justify-content-between my-4">
      <div class="col-8 col-md-6">
        <img class="img-fluid rounded" :src="products.image" alt="" />
      </div>
      <div class="col-4 col-md-6 product-info">
        <h1>{{ products.product }}</h1>
        <p>
          {{
            products.stock > 10
              ? "In Stock"
              : products.stock < 10 && products.stock > 0
              ? "Minimum Stock"
              : "Out of Stock"
          }}
        </p>
        <ul>
          <li v-for="detail of products.details">{{ detail }}</li>
        </ul>
        <div
          v-for="variant in products.variants"
          :key="variant.id"
          @mouseover="products.updateImage(variant.image)"
        >
          {{ variant.color }}
        </div>
        <div class="addCart mt-2">
          <a-button type="default" class="d-flex align-items-center"
            >Add To Cart</a-button
          >
        </div>
      </div>
    </div>
  </main>
</template>

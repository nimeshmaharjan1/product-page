<script setup>
import { ref, computed, reactive, onMounted } from "vue";
import greenSock from "../../assets/images/socks_green.jpg";
import blueSock from "../../assets/images/socks_blue.jpg";
const cart = ref(0);
const props = defineProps({
  premium: Boolean,
});
onMounted(() => {
  console.log(cart.value);
  console.log(props.premium);
});
const products = reactive({
  product: "Socks",
  brand: "Vue Mastery",
  selectedVariant: 0,
  details: ["50% cotton", "30% wool", "20% polyester"],
  variants: [
    { id: 1, color: "green", image: greenSock, quantity: 100 },
    { id: 2, color: "blue", image: blueSock, quantity: 0 },
  ],
  updateVariant: function (index) {
    this.selectedVariant = index; //! changes value of the above selected variant
    console.log(index);
  },
});
const title = computed(() => `${products.brand} ${products.product}`);
const image = computed(() => products.variants[products.selectedVariant].image); //variant[1] or variant[2] based on the mouseover
const inStock = computed(
  () => products.variants[products.selectedVariant].quantity
);
</script>
<template>
  <main class="container">
    <div class="row justify-content-between my-4">
      <div class="col-8 col-md-6">
        <img class="img-fluid rounded" :src="image" alt="" />
      </div>
      <div class="col-4 col-md-6 product-info">
        <h1>{{ title }}</h1>
        <p :class="{ red: !inStock }">
          {{
            inStock > 10
              ? "In Stock"
              : inStock < 10 && inStock > 0
              ? "Minimum Stock"
              : "Out of Stock"
          }}
        </p>
        <p>Shipping {{ premium ? "Free" : "2.99$" }}</p>
        <ul>
          <li v-for="detail of products.details">{{ detail }}</li>
        </ul>
        <div class="d-flex gap-2">
          <button
            class="color-circle"
            v-for="(variant, index) in products.variants"
            :key="variant.id"
            @click="products.updateVariant(index)"
            :style="{ backgroundColor: variant.color }"
          ></button>
        </div>
        <div class="row addCart mt-3">
          <a-button
            @click="$emit('increaseBy', 1)"
            :disabled="!inStock"
            type="primary"
            size="medium"
            class="col-sm-10 d-flex justify-content-center align-items-center"
            >Add To Cart</a-button
          >
          <div class="col-sm-2">
            <a-button
              @click="$emit('clear', 0)"
              class="d-flex justify-content-center align-items-center"
              type="danger"
              >Clear</a-button
            >
          </div>
        </div>
      </div>
    </div>
  </main>
</template>
<style>
.green {
  color: green;
}
.red {
  color: red;
}
</style>

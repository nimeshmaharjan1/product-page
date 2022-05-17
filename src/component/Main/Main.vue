<script setup>
import { ref, computed, reactive, onMounted } from "vue";
import greenSock from "../../assets/images/socks_green.jpg";
import blueSock from "../../assets/images/socks_blue.jpg";
import ReviewForm from "./ReviewForm/ReviewForm.vue";
import ReviewList from "./ReviewForm/ReviewList.vue";
import StarFilled from "../Icons/StarFilled.vue";
import StarOutlined from "../Icons/StarOutlined.vue";
const cart = ref([]);
const props = defineProps({
  premium: Boolean,
});

const products = reactive({
  product: "Socks",
  brand: "Vue Mastery",
  price: "$11.99",
  selectedVariant: 0,
  details: ["50% cotton", "30% wool", "20% polyester"],
  variants: [
    { id: 1, color: "green", image: greenSock, quantity: 100 },
    { id: 2, color: "blue", image: blueSock, quantity: 0 },
  ],
  reviews: [],
  updateVariant: function (index) {
    this.selectedVariant = index; //! changes value of the above selected variant
  },
});
const title = computed(() => `${products.brand} ${products.product}`);
const image = computed(() => products.variants[products.selectedVariant].image); //variant[1] or variant[2] based on the mouseover
const inStock = computed(
  () => products.variants[products.selectedVariant].quantity
);
const addReview = (review) => {
  products.reviews.push(review);
};
let showReview = ref(false);
const giveFeedback = () => {
  showReview = true;
  console.log(showReview);
};
</script>
<template>
  <main class="container">
    <div class="row justify-content-between my-4 mb-5 product-screen">
      <div
        class="col-8 pt-3 pb-4 col-md-6 d-flex justify-content-center align-items-center"
      >
        <img class="img-fluid rounded" :src="image" alt="socks" />
      </div>
      <div class="col-4 col-md-6 product-info">
        <h1 class="product-title py-3 mb-3" style="margin-left: -0.75rem">
          {{ title }}
        </h1>
        <p class="font-weight-bold my-2 mb-3">{{ products.price }}</p>
        <div class="d-flex align-items-center gap-1" style="color: #edb94a">
          <StarFilled />
          <StarFilled />
          <StarFilled />
          <StarFilled />
          <StarOutlined />
          <span style="color: black">8 reviews</span>
        </div>
        <p class="mt-3 description">
          <i>100% cotton, unrefined & organic.</i>
        </p>
        <p class="mt-2">
          Lorem ipsum dolor sit amet consectetur adipisicing elit. Voluptas,
          doloremque doloribus quo voluptatibus soluta quisquam et laboriosam
          eligendi quas illo culpa optio totam porro, pariatur quae cum. Minima,
          praesentium quod?
        </p>
        <ul class="mt-3">
          <li v-for="detail of products.details">{{ detail }}</li>
        </ul>
        <p :class="{ red: !inStock }">
          {{
            inStock > 10
              ? "In Stock"
              : inStock < 10 && inStock > 0
              ? "Minimum Stock"
              : "Out of Stock"
          }}
        </p>
        <div class="d-flex gap-2">
          <button
            class="color-circle"
            v-for="(variant, index) in products.variants"
            :key="variant.id"
            @click="products.updateVariant(index)"
            :style="{ backgroundColor: variant.color }"
          ></button>
        </div>
        <p class="mt-2">Shipping {{ premium ? "Free" : "$ 2.99" }}</p>
        <p
          @click="giveFeedback"
          class="mt-2"
          style="text-decoration: underline; cursor: pointer"
          v-if="!showReview"
        >
          Give a review?
        </p>
        <div class="row addCart mt-3">
          <a-button
            @click="
              $emit(
                'increaseBy',
                products.variants[products.selectedVariant].id
              )
            "
            :disabled="!inStock"
            type="primary"
            size="large"
            class="col-md-10 col-4 d-flex justify-content-center align-items-center"
            >Add</a-button
          >
          <div class="col-md-2 col-8">
            <a-button
              @click="$emit('clear', 0)"
              class="d-flex justify-content-center align-items-center"
              type="primary"
              danger
              ghost
              size="large"
              >Clear</a-button
            >
          </div>
        </div>
      </div>
    </div>
    <!-- <div class="row" v-if="showReview"> -->
    <div class="row">
      <div class="col-sm-6 col-md-6">
        <div class="card">
          <div class="card-header">
            <h2>Your Feedback</h2>
          </div>
          <div class="card-body">
            <ReviewForm @reviewSubmitted="addReview" />
          </div>
        </div>
      </div>
      <div class="col-6">
        <ReviewList :reviews="products.reviews"></ReviewList>
      </div>
    </div>
  </main>
</template>
<style>
/* .product-screen {
  margin-top: 5rem !important;
} */
.green {
  color: green;
}
.red {
  color: red;
}
</style>

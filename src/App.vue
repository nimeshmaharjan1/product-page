<script setup>
import { computed, onMounted, ref } from "vue";
import Header from "./component/Header.vue";
import Footer from "./component/Footer.vue";
import Main from "./component/Main/Main.vue";
import ReviewFormVue from "./component/Main/ReviewForm/ReviewForm.vue";
const premium = ref(false);
const cart = ref([]);
const updateCart = (id) => {
  cart.value.push(id);
};
const clear = () => {
  cart.value = [];
};
let showPreview = ref(false);
</script>
<template>
  <a-layout class="layout">
    <a-layout-header>
      <Header :cartNumber="cart"></Header>
    </a-layout-header>
    <a-layout-content>
      <Main
        class="main-section pb-5"
        :cart="cart"
        :premium="premium"
        @increaseBy="updateCart"
        @clear="clear"
      ></Main>
      <hr />
    </a-layout-content>
    <a-layout-footer>
      <Footer></Footer>
    </a-layout-footer>
  </a-layout>
</template>

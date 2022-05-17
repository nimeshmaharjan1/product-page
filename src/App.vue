<script setup>
import { computed, onMounted, ref } from "vue";
import Header from "./component/Header.vue";
import Footer from "./component/Footer.vue";
import Main from "./component/Main/Main.vue";

const premium = ref(false);
const cart = ref(0);
const updateCart = (n) => {
  return (cart.value += n);
};
const clear = (n) => {
  return (cart.value = 0);
};
</script>
<template>
  <a-layout class="layout">
    <a-layout-header>
      <Header :cartNumber="cart"></Header>
    </a-layout-header>
    <a-layout-content class="main-section">
      <Main
        :cart="cart"
        :premium="premium"
        @increaseBy="updateCart"
        @clear="clear"
      ></Main>
      <p>{{ cart }}</p>
    </a-layout-content>
    <hr />
    <a-layout-footer>
      <Footer></Footer>
    </a-layout-footer>
  </a-layout>
</template>

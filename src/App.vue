<template>
  <a-layout class="layout">
    <a-layout-header>
      <Header></Header>
    </a-layout-header>
    <a-layout-content class="main-section">
      <Main></Main>
    </a-layout-content>
    <hr />
    <a-layout-footer>
      <Footer></Footer>
    </a-layout-footer>
  </a-layout>
</template>
<script setup>
import { ref } from "vue";
import Header from "./component/Header.vue";
import Footer from "./component/Footer.vue";
import Main from "./component/Main.vue";
const product = ref("Socks");
const image = ref("./assets/images/socks_green.jpg");
</script>

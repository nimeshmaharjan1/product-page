<template>
  <header class="d-flex justify-content-between align-items-center">
    <nav class="d-flex gap-4">
      <p>Home</p>
      <p>About</p>
    </nav>
    <div class="cart">
      <a-button class="d-flex align-items-center" shape="round" type="primary">
        <template #icon> <ShoppingCartOutlined /> </template>Cart</a-button
      >
    </div>
  </header>
</template>
<script setup>
import { ShoppingCartOutlined } from "@ant-design/icons-vue";
</script>

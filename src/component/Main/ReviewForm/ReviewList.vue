<script setup>
const props = defineProps({
  reviews: Array,
});
</script>
<template>
  <div class="card">
    <div class="card-header">
      <h2>Reviews</h2>
    </div>
    <div class="card-body">
      <ul>
        <li v-for="(review, index) in props.reviews" :key="index">
          {{ review.name }}
        </li>
      </ul>
    </div>
  </div>
</template>

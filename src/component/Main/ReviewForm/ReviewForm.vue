<template>
  <a-form
    class="mt-4"
    :model="formState"
    name="basic"
    :label-col="{ span: 7 }"
    :wrapper-col="{ span: 13 }"
    autocomplete="off"
    @submit.prevent="onSubmit"
  >
    <a-form-item
      label="Name"
      name="name"
      :rules="[{ required: true, message: 'Please input your name!' }]"
    >
      <a-input placeholder="Enter your name" v-model:value="formState.name" />
    </a-form-item>

    <a-form-item
      label="Review"
      name="review"
      :rules="[{ required: true, message: 'Please input your review!' }]"
    >
      <a-textarea
        v-model:value="formState.review"
        placeholder="Enter your review"
        allow-clear
        :rules="[{ required: true, message: 'Please input your review!' }]"
      />
    </a-form-item>
    <a-form-item
      label="Rating"
      name="rating"
      :rules="[{ required: true, message: 'Please input your rating!' }]"
    >
      <a-select
        placeholder="Enter your rating"
        ref="select"
        v-model:value="formState.rating"
      >
        <a-select-option value="1">1</a-select-option>
        <a-select-option value="2">2</a-select-option>
        <a-select-option value="3">3</a-select-option>
        <a-select-option value="4">4</a-select-option>
        <a-select-option value="5">5</a-select-option>
      </a-select>
    </a-form-item>

    <a-form-item :wrapper-col="{ offset: 11, span: 16 }">
      <a-button
        type="primary"
        class="d-flex align-items-center"
        html-type="submit"
        @click="$emit('reviewSubmitted', productReview)"
        >Submit</a-button
      >
    </a-form-item>
  </a-form>
</template>
<script setup>
import { reactive } from "vue";
let productReview = reactive({});
const formState = reactive({
  name: "",
  review: "",
  rating: null,
});
const onSubmit = () => {
  productReview = {
    name: formState.name,
    review: formState.review,
    rating: Number(formState.rating),
  };
};
</script>
<style></style>

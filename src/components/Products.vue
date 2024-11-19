<script setup>

import { ref, onMounted } from 'vue';
import axios from 'axios';

const products = ref([]);

const getAllProducts = async () => {
  try {
    const response = await axios.get("http://localhost:5000/products");
    console.log(response.data);
    products.value = response.data;
  } catch (err) {
    console.log(err);
  }
};

onMounted(() => {
  getAllProducts();
});

</script>

<template>
  <div>
    <ul>
      <li v-for="product in products" :key="product.productID">{{ product.productName }}</li>
    </ul>
  </div>
</template>

<style scoped>

</style>
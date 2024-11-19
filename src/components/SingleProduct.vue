<script setup>
import {ref, onMounted} from "vue";
import axios from 'axios';

const input = ref('');
const product = ref(null);
const fejlbesked = ref('');

const getProductByID = async () => {
  const pId = input.value;
  fejlbesked.value = '';

  if (!pId) {
    fejlbesked.value = "Du har ikke skrevet et id spade!"
    return
  }

  try {
    const response = await axios.get("http://localhost:5000/products/" + pId);
    console.log(response.data);
    product.value = response.data;
  } catch (err) {
    console.log(err);
    fejlbesked.value = 'Kunne ikke finde en frugt med dét id...'
  }
};

const getproduct = () => {
  console.log(input.value);
}
</script>

<template>
  <div>
    <label for="product">Type product ID</label>
    <input type="text" name="product" v-model="input">
    <button type="submit" @click="getProductByID">Submit ID</button>
  </div>
  <div>
    <p>{{fejlbesked ? fejlbesked : product}}</p>
  </div>
</template>

<style scoped>

</style>
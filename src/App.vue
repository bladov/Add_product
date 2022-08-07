<template>
  <div class="container">
    <FormAddProduct @addProduct="takeProduct($event)" />
    <ProductList :product="product" />
  </div>
</template>

<script setup>
import { ref } from 'vue';
import FormAddProduct from './components/FormAddProduct.vue';
import ProductList from './components/ProductList.vue';

const product = ref(null);

const takeProduct = (e) => {
  product.value = e;
};
</script>

<style lang="scss" scoped>
.container {
  margin: 0 auto;
  padding: 0 32px;
  max-width: 1504px;
  display: flex;
  column-gap: 16px;
}
</style>

<template>
  <div class="container">
    <FormAddProduct />
    <ProductList />
  </div>
</template>

<script setup>
import FormAddProduct from './components/FormAddProduct.vue';
import ProductList from './components/ProductList.vue';
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

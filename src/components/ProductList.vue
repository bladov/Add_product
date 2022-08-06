<template>
  <section class="Product-list">
    <select name="list" id="" class="filter">
      <option value="1">1</option>
      <option value="2">2</option>
      <option value="3">3</option>
    </select>

    <ul>
      <li class="item">cgbcjr</li>
      <li class="item">cgbcjr2</li>
      <li class="item">cgbcjr3</li>
    </ul>
  </section>
</template>

<script>
export default {};
</script>

<style scoped lang="scss">
.Product-list {
  margin: 0;
  padding-top: 32px;

  display: flex;
  flex-direction: column;
  flex-grow: 1;
}

.filter {
  margin: 0;
  justify-self: end;
  align-self: end;
}

ul {
  margin: 0;
  list-style-type: none;
}

.item {
  border: 1px solid red;
}
</style>

<template>
  <section class="Product-list">
    <select name="list" id="" class="filter">
      <option value="1">По умолчанию</option>
      <option value="1">По уменьшанию</option>
      <option value="3">По возрастанию</option>
      <option value="3">По наименованию</option>
    </select>

    <ul>
      <li class="item">По умолчанию</li>
      <li class="item">По уменьшанию</li>
      <li class="item">По возрастанию</li>
      <li class="item">По наименованию</li>
    </ul>
  </section>
</template>

<script>
export default {};
</script>

<style scoped lang="scss">
@import '@/scss/variables';

.Product-list {
  margin: 0;
  padding-top: 32px;

  display: flex;
  flex-direction: column;
  flex-grow: 1;
}

.filter {
  margin: 0 0 16px 0;
  justify-self: end;
  align-self: end;
  padding: 10px 0 10px 16px;

  font-size: 12px;
  line-height: 15px;
  color: $grey-03;

  background: $white-01;
  box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
  border: none;
  border-radius: 4px;

  &:hover {
    box-shadow: 0px 2px 5px rgba(5, 163, 236, 0.986);
  }

  &:focus {
    outline: 1px solid rgba(5, 163, 236, 0.986);
  }
}

ul {
  margin: 0;
  list-style-type: none;
}

li {
  margin: 0;
}

.item {
  border: 1px solid red;
}
</style>

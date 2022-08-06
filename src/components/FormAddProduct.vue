<template>
  <section class="Product">
    <h1 class="Product__title">Добавление товара</h1>

    <form class="Product__form">
      <label class="Product__label" for="productTitle"> Наименование товара </label>
      <input id="productTitle" class="Product__input" type="text" required placeholder="Введите наименование товара" />

      <label class="Product__label" for="description"> Описание товара </label>
      <textarea id="description" class="Product__input" placeholder="Введите описание товара" />

      <label class="Product__label" for="picture"> Ссылка на изображение товара </label>
      <input id="picture" class="Product__input" type="text" required placeholder="Введите ссылку" />

      <label class="Product__label" for="price"> Цена товара </label>
      <input id="price" class="Product__input" type="text" required placeholder="Введите цену" />

      <button class="Product__btn" type="submit">Добавить товар</button>
    </form>
  </section>
</template>

<script setup></script>

<style scoped lang="scss">
@import '@/scss/variables';

.Product {
  margin: 0;
  padding-top: 32px;

  &__title {
    margin-bottom: 16px;
    color: $grey-01;
    font-weight: 600;
    font-size: 28px;
    line-height: 35px;

    @media (max-width: 868px) {
      font-size: 18px;
    }
  }

  &__form {
    padding: 24px;
    margin: 0;
    max-width: 332px;
    background: $white-01;
    box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04), 0px 6px 10px rgba(0, 0, 0, 0.02);
    border-radius: 4px;
  }

  &__label {
    display: inline-block;
    margin-bottom: 4px;
    font-size: 10px;
    line-height: 13px;
    letter-spacing: -0.02em;
    color: $grey-02;
  }

  &__input {
    display: inline-block;
    width: 100%;
    border: none;
    padding: 10px 16px;
    margin-bottom: 16px;
    background: $white-01;
    box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
    border-radius: 4px;
    font-size: 12px;
    line-height: 15px;
    transition: all 0.2s ease-in-out;

    color: $grey-01;

    &::placeholder {
      font-size: 12px;
      line-height: 15px;
      text-align: left;
      color: $grey-03;
    }

    &:hover {
      box-shadow: 0px 2px 5px rgba(5, 163, 236, 0.986);
    }

    &:focus {
      outline: 1px solid rgba(5, 163, 236, 0.986);
    }
  }

  &__btn {
    width: 100%;
    display: block;
    padding: 10px 0;
    margin-top: 8px;
    background: $white-02;
    border-radius: 10px;
    border: none;

    font-weight: 600;
    font-size: 12px;
    line-height: 15px;
    text-align: center;
    letter-spacing: -0.02em;
    color: $grey-03;
    transition: all 0.2s ease-in-out;

    &:hover {
      background: rgb(53, 177, 226);
      color: black;
    }
  }
}

textarea {
  max-width: 284px;
  max-height: 108px;
}

label {
  position: relative;
}

label:not(:nth-child(3))::before {
  content: '';
  display: block;
  position: absolute;
  right: -5px;
  top: 0;
  width: 4px;
  height: 4px;
  background: #ff8484;
  border-radius: 4px;
}
</style>

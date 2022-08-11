<template>
  <section class="Product">
    <h1 class="Product__title">Добавление товара</h1>

    <form class="Product__form" @submit.prevent>
      <label class="Product__label required" for="productTitle"> Наименование товара </label>
      <input
        v-model="product.title"
        id="productTitle"
        class="Product__input"
        type="text"
        required
        placeholder="Введите наименование товара"
      />

      <label class="Product__label" for="description"> Описание товара </label>
      <textarea
        v-model="product.description"
        id="description"
        class="Product__input"
        placeholder="Введите описание товара"
      />
      <label class="Product__label required" for="picture"> Ссылка на изображение товара </label>
      <input
        v-model="product.url"
        required
        id="picture"
        class="Product__input"
        type="text"
        placeholder="Введите ссылку"
      />

      <label class="Product__label required" for="price"> Цена товара </label>
      <input
        v-model="product.price"
        id="price"
        class="Product__input"
        type="number"
        required
        placeholder="Введите цену"
      />

      <button
        @click="addProduct"
        class="Product__btn"
        :class="{ 'Product__btn-active': activeBtn }"
        :disabled="!activeBtn"
        type="submit"
      >
        Добавить товар
      </button>
    </form>
  </section>
</template>

<script setup>
import { computed, reactive } from 'vue';

const keys = Object.keys(localStorage);
let lastId = Math.max(...keys);

if (!isFinite(lastId)) {
  lastId = 0;
}

const product = reactive({
  title: null,
  description: null,
  url: null,
  price: null,
  id: lastId,
});

const emit = defineEmits(['addProduct']);

const activeBtn = computed(() => {
  return !!product.title && !!product.price && !!product.url;
});

const addProduct = () => {
  product.id += 1;

  if (!product.url.startsWith('https')) {
    product.url = null;
  }

  emit('addProduct', { ...product });

  for (let key in product) {
    if (key === 'id') {
      continue;
    }
    product[key] = '';
  }
};
</script>

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

    &-active {
      background: #7bae73;
      color: #ffffff;

      &:hover {
        background: #4fe738;
      }
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

.required::before {
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

<template>
  <section class="Product-list">
    <select v-model="filter" name="list" id="" class="filter">
      <option value="defualt">По умолчанию</option>
      <option value="min">По уменьшанию</option>
      <option value="max">По возрастанию</option>
      <option value="name">По наименованию</option>
    </select>

    <ul class="list">
      <li
        v-for="(product, index) in feltredProducts"
        :key="index"
        class="item"
        :class="{ delete: product.hover }"
        @mousemove="addHover(index)"
        @mouseleave="deketeHover(index)"
        @click="deleteProduct(index, product)"
      >
        <div class="bin" v-if="product.hover">
          <svg width="16" height="16" viewBox="0 0 16 16" fill="none" xmlns="http://www.w3.org/2000/svg">
            <g clip-path="url(#clip0_12_141)">
              <path
                d="M10.207 5.79681C10 5.79681 9.83228 5.96455 9.83228 6.17152V13.2535C9.83228 13.4603 10 13.6282 10.207 13.6282C10.4139 13.6282 10.5817 13.4603 10.5817 13.2535V6.17152C10.5817 5.96455 10.4139 5.79681 10.207 5.79681Z"
                fill="white"
              />
              <path
                d="M5.78547 5.79681C5.57851 5.79681 5.41077 5.96455 5.41077 6.17152V13.2535C5.41077 13.4603 5.57851 13.6282 5.78547 13.6282C5.99244 13.6282 6.16018 13.4603 6.16018 13.2535V6.17152C6.16018 5.96455 5.99244 5.79681 5.78547 5.79681Z"
                fill="white"
              />
              <path
                d="M2.56301 4.76329V13.9953C2.56301 14.5409 2.76309 15.0534 3.11262 15.421C3.46054 15.7898 3.94473 15.9991 4.45147 15.9999H11.541C12.0479 15.9991 12.5321 15.7898 12.8799 15.421C13.2294 15.0534 13.4295 14.5409 13.4295 13.9953V4.76329C14.1243 4.57887 14.5745 3.90762 14.4816 3.19465C14.3885 2.48183 13.7812 1.94861 13.0622 1.94846H11.1438V1.48008C11.146 1.0862 10.9902 0.707978 10.7114 0.429729C10.4326 0.151627 10.0538 -0.00323193 9.65988 -1.18018e-05H6.33261C5.93873 -0.00323193 5.55992 0.151627 5.28109 0.429729C5.00225 0.707978 4.84652 1.0862 4.84871 1.48008V1.94846H2.93025C2.21128 1.94861 1.60399 2.48183 1.5109 3.19465C1.41796 3.90762 1.86819 4.57887 2.56301 4.76329ZM11.541 15.2505H4.45147C3.81081 15.2505 3.31242 14.7002 3.31242 13.9953V4.79623H12.6801V13.9953C12.6801 14.7002 12.1817 15.2505 11.541 15.2505ZM5.59812 1.48008C5.59564 1.28497 5.67233 1.09717 5.8108 0.959441C5.94912 0.821707 6.13735 0.746034 6.33261 0.7494H9.65988C9.85514 0.746034 10.0434 0.821707 10.1817 0.959441C10.3202 1.09703 10.3969 1.28497 10.3944 1.48008V1.94846H5.59812V1.48008ZM2.93025 2.69787H13.0622C13.4348 2.69787 13.7367 2.99983 13.7367 3.37234C13.7367 3.74485 13.4348 4.04681 13.0622 4.04681H2.93025C2.55774 4.04681 2.25578 3.74485 2.25578 3.37234C2.25578 2.99983 2.55774 2.69787 2.93025 2.69787Z"
                fill="white"
              />
              <path
                d="M7.99617 5.79681C7.7892 5.79681 7.62146 5.96455 7.62146 6.17152V13.2535C7.62146 13.4603 7.7892 13.6282 7.99617 13.6282C8.20313 13.6282 8.37087 13.4603 8.37087 13.2535V6.17152C8.37087 5.96455 8.20313 5.79681 7.99617 5.79681Z"
                fill="white"
              />
            </g>
            <defs>
              <clipPath id="clip0_12_141">
                <rect width="16" height="16" fill="white" />
              </clipPath>
            </defs>
          </svg>
        </div>
        <img class="picture" alt="product" :src="product.url ?? picture" @error="error(product)" />
        <div class="description">
          <h2 class="title">{{ product.title }}</h2>
          <p class="text">
            {{ product.description }}
          </p>
          <div class="price">{{ product.price }} руб.</div>
        </div>
      </li>
    </ul>
  </section>
</template>

<script>
import { cloneDeep } from 'lodash';

export default {
  props: {
    product: Object,
  },

  data() {
    return {
      productList: [],
      filter: 'defualt',
    };
  },

  watch: {
    product(val) {
      this.productList.push(val);
      localStorage.setItem(`${val.id}`, JSON.stringify(val));
    },
  },

  created: function () {
    let keys = Object.keys(localStorage);

    for (let key of keys) {
      const product = JSON.parse(localStorage.getItem(key));
      this.productList.push(product);
    }
  },

  computed: {
    feltredProducts() {
      const cloneProduct = cloneDeep(this.productList);
      if (this.filter === 'max') {
        return cloneProduct.sort((a, b) => +a.price - +b.price);
      }
      if (this.filter === 'min') {
        return cloneProduct.sort((a, b) => +b.price - +a.price);
      }

      if (this.filter === 'name') {
        return cloneProduct.sort((a, b) => +b.title.length - +a.title.length);
      }
      return this.productList;
    },

    picture() {
      let img = require('@/assets/camera2.png');
      return img;
    },
  },

  methods: {
    addHover(index) {
      this.productList[index].hover = true;
    },
    deketeHover(index) {
      this.productList[index].hover = false;
    },

    deleteProduct(index, product) {
      localStorage.removeItem(+product.id);
      this.productList.splice(index, 1);
    },

    error(prosuct) {
      let img = require('@/assets/camera2.png');
      prosuct.url = img;
    },
  },
};
</script>

<style scoped lang="scss">
@import '@/scss/variables';

.Product-list {
  margin: 0;
  padding-top: 32px;
  max-width: 1028px;

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

.list {
  margin: 0;
  display: flex;
  flex-wrap: wrap;
  list-style-type: none;
  justify-content: space-between;
  gap: 16px;
}

.item {
  // flex: 0 1 30%;
  align-self: flex-start;
  position: relative;
  margin: 0;
  max-width: 332px;
  background: $white-01;
  box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04), 0px 6px 10px rgba(0, 0, 0, 0.02);
  border-radius: 4px;
}

.delete {
  cursor: pointer;
  animation: deleted 0.5s;
}

.bin {
  position: absolute;
  text-align: center;
  top: -10px;
  right: -10px;
  width: 32px;
  height: 32px;
  background: #ff8484;
  box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
  border-radius: 10px;
}

.picture {
  display: block;
  max-width: 100%;
  max-height: 100%;
  margin-bottom: 16px;
  object-fit: contain;
}

.description {
  padding: 0 16px 24px 16px;
}
.title {
  margin-bottom: 16px;
  font-weight: 600;
  font-size: 20px;
  line-height: 25px;
  color: $grey-01;
}
.text {
  margin-bottom: 32px;
  font-size: 16px;
  line-height: 20px;
  color: $grey-01;
}
.price {
  font-weight: 600;
  font-size: 24px;
  line-height: 30px;

  color: $grey-01;
}

@keyframes deleted {
  25% {
    transform: rotateY(20deg);
  }

  50% {
    transform: rotateY(0);
  }

  75% {
    transform: rotateY(-20deg);
  }

  100% {
    transform: rotateY(0);
  }
}
</style>

<template>
  <div class="navbar">
    <a>Home</a>
    <a>Products</a>
    <a>About</a>
    <div class="cart-container">
      <img class="cart-icon" alt="cart icon" src="./assets/svgs/cart.svg" />
      <span>{{ cartCount }}</span>
    </div>
  </div>

  <img class="vue-logo" alt="Vue logo" src="./assets/images/logo.png" />

  <!-- modal -->
  <AlertModal v-if="modalIsOpen === true" @on-close="closeModal" />

  <!-- products -->
  <div>
    <h1>Products List</h1>

    <!-- 상품 목록 -->
    <ul class="product-container">
      <li class="product" v-for="(product, i) in products" :key="i">
        <h2 class="product-name">{{ product.name }}</h2>
        <p>{{ product.description }}</p>
        <div class="button-container">
          <button class="detail-btn" @click="openModal">Detail</button>
          <button class="add-cart-btn" @click="increaseCart">Add Cart</button>
        </div>
      </li>
    </ul>
  </div>
</template>

<!-- composition API -->
<script setup>
import { ref, onMounted } from "vue";

import AlertModal from "./components/AlertModal.vue";

const modalIsOpen = ref(false);
const cartCount = ref(0);
const products = ref([
  {
    name: "Product 1",
    description: "Product 1 Description",
  },
  {
    name: "Product 2",
    description: "Product 2 Description",
  },
]);

function increaseCart() {
  cartCount.value++;
}

function openModal() {
  modalIsOpen.value = true;
}

function closeModal() {
  modalIsOpen.value = false;
}
// 생명 주기 훅
onMounted(() => {
  console.log("mounted");
});
</script>

<style>
#app {
  font-family: JetBrains Mono, "Pretendard", sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
}
.navbar {
  display: flex;
  width: 80%;
  justify-content: center;
  margin: 0 auto;
  gap: 30px;
  padding: 20px;
  border-bottom: 1px solid rgba(255, 255, 255, 0.2);
}
.navbar a {
  font-size: 20px;
  text-decoration: none;
}
.vue-logo {
  margin-top: 20px;
  width: 100px;
  height: 100px;
}
.cart-container {
  display: flex;
  align-items: center;
  position: relative;
  gap: 5px;
}
.cart-icon {
  width: 22px;
  height: 25px;
  cursor: pointer;
}
.product-container {
  display: flex;
  flex-direction: column;
  flex-wrap: wrap;
  gap: 20px;
  margin-top: 40px;
  justify-content: center;
  align-items: center;
}
.product {
  width: 300px;
  padding: 20px;
  border-radius: 15px;
  box-shadow: 0px 0px rgba(255, 255, 255, 0.1);
  border: 1px solid rgba(255, 255, 255, 0.1);
}
.product-name {
  font-weight: 600;
  margin-top: 0;
}
.button-container {
  display: flex;
  gap: 10px;
  margin-top: 20px;
  justify-content: center;
  align-items: center;
}
.detail-btn {
  padding: 5px 10px;
  background-color: transparent;
  border: none;
  border-radius: 15px;
  cursor: pointer;
  font-family: JetBrains Mono;
  font-size: 13px;
  line-height: 23px;
  color: white;
  text-align: center;
  font-weight: 500;
  border: 1px solid white;
}
.add-cart-btn {
  padding: 5px 10px;
  background-color: #167dff;
  border: none;
  border-radius: 15px;
  cursor: pointer;
  font-family: JetBrains Mono;
  font-size: 13px;
  line-height: 23px;
  color: white;
  text-align: center;
}
</style>

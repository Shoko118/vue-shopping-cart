<script setup>
import { ref } from "vue";

const products = [
  { id: 1, name: "Guitar capo", price: 12, description: "lorem ipsum..." },
  { id: 2, name: "Washing machine", price: 70, description: "lorem ipsum..." },
  { id: 3, name: "Books", price: 50, description: "lorem ipsum..." },
  { id: 4, name: "Calculator", price: 20, description: "lorem ipsum..." },
];

// reactive variables
const carts = ref([]);
const page = ref("products");

// functionality
function addProduct(product) {
  // the array of carts I want to push each of the element of the product
  return carts.value.push(product);
}

function navigateTo(navigate) {
  page.value = navigate;
}

function removeProduct(index) {
  carts.value.splice(index, 1);
}
</script>

<template>
  <div>
    <header>
      <h1>THE SHOPPING CART WEB</h1>
      <button @click="navigateTo('products')">Shopping cart</button>
      <button @click="navigateTo('cart')">View Cart</button>
    </header>

    <ul>
      <li v-if="page === 'products'" v-for="(product, i) in products" key="i">
        <h2>The {{ product.name }}</h2>
        <h3>${{ product.price }}</h3>
        <p>Description: {{ product.description }}</p>
        <button @click="addProduct(product)">Add</button>
      </li>
    </ul>

    <div v-if="page === 'cart'">
      <div>
        <h2 v-if="carts.length === 0">The cart is empty</h2>
        <h2 v-else>
          HERE ARE THE CARTS {{ carts.length }}
          <ul>
            <li v-for="(cart, index) in carts" key="index">
              <h2>The {{ cart.name }}</h2>
              <h3>${{ cart.price }}</h3>
              <p>Description: {{ cart.description }}</p>
              <button @click="removeProduct(index)">Delete</button>
            </li>
          </ul>
        </h2>
      </div>
    </div>
  </div>
</template>

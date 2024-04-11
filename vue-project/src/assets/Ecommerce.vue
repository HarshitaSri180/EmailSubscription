<!-- YourComponent.vue -->

<template>
  <div class="ApiFetch">
    <button @click="getProducts">Get Products</button>
    <div v-if="products">
      <ul class="product-list">
        <li v-for="product in products" :key="product.id" class="product-item">
          <div>
            <img :src="product.image" alt="Product Image" />
            <div class="product-details">
              <p>{{ product.title }}</p>
              <p>{{ "$"+product.price }}</p>
              <p >{{ product.description}}</p>
            </div>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue';
import { fetchProducts } from './Api'; // Adjust the path based on your project structure

export default {
  setup() {
    const products = ref(null);

    const getProducts = async () => {
      try {
        products.value = await fetchProducts();
      } catch (error) {
        // Handle errors
        console.error('Error fetching products:', error);
      }
    };
    
    return {
      products,
      getProducts,
    };
  },
};
</script>

<style scoped>
img {
    height: 30vh;
    border-radius: 8px;
    width: 16vw;
    margin: 18px;
}

ul {
    list-style: none;
    display: flex;
    flex-wrap: wrap;
    /* justify-content: space-around; */
    padding: 0;
}

.product-item {
    width: 30%; /* Set the width to fit three items in a row */
    margin-bottom: 20px;
}
.product-details{
  width:58%;
}

.ApiFetch {
    background-color: rgb(207, 134, 38);
}
</style>

<template>
  <div class="container">
    <div class="products">
      <div>
        <h1>New products</h1>
        <p>Choose the headset that best suits your needs. We offer top-quality options with <br> a variety of features to enhance your audio experience</p>
      </div>
      <div class="p-card-box">
        <div v-for="product in products" :key="product.id" class="p-card">

          <img class="" :src="getImageUrl(product.image_url)" alt="">
          <p>{{ product.description }}</p>
          <div class="price">
            <span class="s">$</span><h1>{{ product.price }}</h1><span class="red">${{ product.originalPrice }}</span>
          </div>
          <button class="btn_hero">add to cart <div class="btn-ball"><i class="bi bi-cart3"></i></div></button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      products: [],
     
      imageBaseUrl: 'https://localhost:7119/' 
    };
  },
  mounted() {
    this.fetchProducts();
  },
  methods: {
    async fetchProducts() {
      try {
        const response = await axios.get('https://localhost:7119/api/Produto');
        this.products = response.data;
      } catch (error) {
        console.error('Error fetching products:', error);
      }
    },
    // Função que retorna a URL completa para a imagem
    getImageUrl(imagePath) {
      return `${this.imageBaseUrl}${imagePath}`;
    }
  }
};
</script>

<style scoped>
  *  img {
    width: 400px;
  }
</style>

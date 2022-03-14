<template>
  <div class="home">
    <div>
      <span style="color: black; font-size: 30px;"><b>Listado de productos</b></span>
      <template>
        <div>
          <section class="wrapper">
            <ul class="products">
              <li style="border: black 3px solid; width: 450px; display:inline-grid; margin:20px;"
                v-for="product in products"
                :key="product.id"
                class="products__product">
                <img class="product-image" :src="product.mainImage" alt="" width="100%"/>
                <p class="product-title" style="margin-top: 40px; font-size: 20px; color: black;"><b>{{ product.name }}</b></p>
                <p>
                  <em style="color: black; font-size: 17px">${{ product.price }}</em>
                </p>
                <div style="display: flex;">
                  <b-button style="width: 45%; background-color: #319EB9;"><router-link :to="{name: 'details', params: {id: product.id}}" style="text-decoration: none; color: black"><b>Details</b></router-link></b-button>
                  <b-button @click="$router.push('/cart')" style="width: 45%; margin-left: 10%; color: black; background-color: #60B931;"><b>Add to cart</b></b-button>
                </div>
              </li>
            </ul>
          </section>
        </div>
      </template>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from '@/components/HelloWorld.vue'

import api_url from "../utils/api";

export default {
  name: 'Home',

  components: {
  },
  created() {
    fetch(api_url("/products"))
      .then((result) => result.json())
      .then((data) => (this.products = data));
  },
  data() {
    return {
      products: [],
    };
  },
}
</script>

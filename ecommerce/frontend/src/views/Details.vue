<template>
  <div class="details">
    <div>
      <span style="color: black; font-size: 30px;"><b>Detalles del producto: {{product.id}}</b></span>
      <template>
        <div>
          <section class="wrapper">
            <ul class="products">
              <li style="border: black 3px solid; width: 450px; display:inline-grid; margin:20px;" class="products__product">
                <img class="product-image" :src="product.mainImage" alt="" width="100%"/>
                <p class="product-title" style="margin-top: 40px; font-size: 20px; color: black;"><b>{{ product.name }}</b></p>
                <p>
                  <em style="color: black; font-size: 17px">${{ product.price }}</em>
                </p>
                <p>
                  ${{ product.description }}
                </p>
                <div style="display: flex;">
                  <router-link :to="{name: 'Home'}" style="text-decoration: none; width: 45%"><b-button style="width: 100%; background-color: #319EB9; color: black"><b>Back to Home</b></b-button></router-link>
                  <b-button @click="addToCart" style="width: 45%; margin-left: 11%; background-color: #60B931; color: black"><b>Add to cart</b></b-button>
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
import api_url from "../utils/api";

export default {
  name: 'details',
  components: {
  },
  created() {
    this.getProductById(this.$route.params.id)
  },
  beforeRouteUpdate(to,from){
    this.getProductById(to.params.id)
  },
  data() {
    return {
      product: [],
    };
  },
  methods: {
    getProductById(id) {
      fetch(api_url("/products/" + id))
      .then((result) => result.json())
      .then((data) => (this.product = data));
    },
    addToCart() {
      fetch(api_url("/cart/", {
        method: "POST",
        body: JSON.stringify({"productId":0,"quantity":1}),
        }))
    }
  }
};
</script>
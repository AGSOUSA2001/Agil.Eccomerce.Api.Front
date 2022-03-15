<template>
  <div class="home">
    <div>
      <span style="color: black; font-size: 30px"><b>Carrito</b></span>
      <template>
        <div>
          <section class="wrapper">
            <ul
              style="
                display: inline-grid;
                justify-content: center;
                align-items: center;
                margin-top: 70px;
              "
            >
              <li
                v-for="product in products"
                :key="product.id"
                style="
                  border: black 3px solid;
                  width: 850px;
                  display: flex;
                  justify-content: center;
                  align-items: center;
                  padding-top: 15px;
                  margin-bottom: 40px;
                "
              >
                <p>{{ product.productName }}</p>
                <p style="padding: 0px 200px">{{ product.productPrice }}</p>
                <p style="padding-right: 100px">{{ product.quantity }}</p>
                <b-button
                  @click="
                    upgradeQuantity(
                      product.id,
                      product.quantity,
                      product.productId,
                      product.productName,
                      product.productPrice
                    )
                  "
                  style="
                    margin-right: 10px;
                    width: 40px;
                    background-color: #46a0f0;
                    color: black;
                    margin-top: -15px;
                  "
                  ><b>+</b></b-button
                >
                <b-button
                  @click="
                    degradeQuantity(
                      product.id,
                      product.quantity,
                      product.productId,
                      product.productName,
                      product.productPrice
                    )
                  "
                  style="
                    width: 40px;
                    background-color: #f04646;
                    color: black;
                    margin-top: -15px;
                  "
                  ><b>-</b></b-button
                >
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
  name: "Cart",

  components: {},
  created() {
    fetch(api_url("/cart/"))
      .then((result) => result.json())
      .then((data) => (this.products = data));
  },
  data() {
    return {
      products: [],
    };
  },
  methods: {
    upgradeQuantity(id, quantity, productId, productName, productPrice) {
      fetch(api_url("/cart/" + id), {
        method: "PUT",
        body: JSON.stringify({
          productId: productId,
          productName: productName,
          quantity: quantity + 1,
          productPrice: productPrice,
        }),
        headers: {
          "Content-Type": "application/json",
          // 'Content-Type': 'application/x-www-form-urlencoded',
        },
      });
      fetch(api_url("/cart/"))
        .then((result) => result.json())
        .then((data) => (this.products = data));
    },
    degradeQuantity(id, quantity, productId, productName, productPrice) {
      if (quantity > 1) {
        fetch(api_url("/cart/" + id), {
          method: "PUT",
          body: JSON.stringify({
            productId: productId,
            productName: productName,
            quantity: quantity - 1,
            productPrice: productPrice,
          }),
          headers: {
            "Content-Type": "application/json",
            // 'Content-Type': 'application/x-www-form-urlencoded',
          },
        });
        fetch(api_url("/cart/"))
          .then((result) => result.json())
          .then((data) => (this.products = data));
      } else {
        fetch(api_url("/cart/" + id), {
          method: "DELETE",
          body: JSON.stringify({
            productId: productId,
            productName: productName,
            quantity: quantity,
            productPrice: productPrice,
          }),
          headers: {
            "Content-Type": "application/json",
            // 'Content-Type': 'application/x-www-form-urlencoded',
          },
        });
        fetch(api_url("/cart/"))
          .then((result) => result.json())
          .then((data) => (this.products = data));
      }
    },
  },
};
</script>
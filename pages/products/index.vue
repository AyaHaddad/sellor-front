<template>
  <v-app>
    <v-container fluid class="py-12">
      <div class="d-flex flex-row justify-start align-start flex-wrap">
        <template>
          <v-col
            xl="3"
            lg="3"
            md="3"
            sm="6"
            xs="12"
            v-for="product in products"
            :key="product._id"
          >
            <div>
              <v-card
                class="s-card-product rounded-lg"
                elevation="4"
                :to="`/products/${product._id}`"
              >
                <v-img
                  :lazy-src="product.image"
                  max-height="200"
                  max-width="500"
                  :src="product.image"
                ></v-img>
                <div class="d-flex flex-row justify-space-between px-5 pt-5">
                  <p class="subtitle-1 mb-0 font-weight-bold">
                    {{ product.name }}
                  </p>

                  <v-chip>
                    <p class="body-1 mb-0 font-weight-bold">
                      {{ product.price }} €
                    </p></v-chip
                  >
                </div>
                <v-card-text>
                  <p class="body-2 text-secondary mb-1">
                    stock : {{ product.stock }}
                  </p>
                </v-card-text>
                <v-divider></v-divider>
                <v-card-actions class="px-7 pb-7 pt-5">
                  <v-row
                    class="d-flex flex-row align-center justify-center full-width"
                  >
                    <v-btn type="submit" color="primary" block text depressed
                      ><v-icon dense class="mr-1">mdi-cart-outline</v-icon
                      >Ajouter au panier
                    </v-btn></v-row
                  >
                </v-card-actions>
              </v-card>
            </div>
          </v-col>
        </template>
      </div>
    </v-container>
  </v-app>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      products: [],
    };
  },

  computed: {
    test() {
      return this.$auth.strategy.token.get();
    },
  },

  mounted() {
    this.$axios
      .get("http://localhost:3000/products", {
        headers: {
          "Content-Type": "application/json",
          "auth-token": this.test.split(" ")[1],
        },
      })
      .then((res) => {
        this.products = res.data;
      })
      .catch((err) => console.log("err", err));
  },
};
</script>

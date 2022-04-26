<template>
  <v-app>
    <v-container fluid class="py-12" v-if="product">
      <div class="d-flex flex-row">
        <v-col xl="6" lg="6" md="6" sm="12" xs="12" class="py-0">
          <v-img :lazy-src="product.image" :src="product.image"></v-img
        ></v-col>
        <v-col xl="6" lg="6" md="6" sm="12" xs="12" class="pa-14">
          <h4 class="display-1 mb-3 font-weight-bold">{{ product.name }}</h4>
          <v-chip>
            <p class="subtitle-1 mb-0 font-weight-bold">
              {{ product.price }} €
            </p></v-chip
          >
          <p class="subtitle-1 text-secondary mt-3">
            Lorem Ipsum is simply dummy text of the printing and typesetting
            industry.
          </p>
          <v-divider class="my-3"></v-divider>
          <v-select
            v-model="e1"
            :items="items"
            placeholder="quantité"
            outlined
            menu-props="auto"
          ></v-select>
          <v-btn type="submit" color="primary" block depressed x-large
            ><v-icon dense class="mr-1">mdi-cart-outline</v-icon>Ajouter au
            panier
          </v-btn>
        </v-col>
      </div>
    </v-container>
  </v-app>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      product: null,
      items: [1, 2, 3, 4, 5],
      e1: 1,
    };
  },

  computed: {
    test() {
      return this.$auth.strategy.token.get();
    },
  },

  created() {
    console.log(this.$route);
    const url = `http://localhost:3000/products/${this.$route.params.id}`;
    this.$axios
      .get(url, {
        headers: {
          "Content-Type": "application/json",
          "auth-token": this.test.split(" ")[1],
        },
      })
      .then((res) => {
        this.product = res.data;
      })
      .catch((err) => console.log("err", err));
  },
};
</script>

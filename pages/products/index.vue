<template>
  <v-app>
    <v-container fluid class="py-12">
      <div class="d-flex flex-row justify-start align-start flex-wrap">
        <template v-for="i in 8">
          <v-col xl="3" lg="3" md="3" sm="6" xs="12">
            <v-card
              class="s-card-product rounded-lg"
              elevation="4"
              to="/products/product"
            >
              <v-img
                lazy-src="https://picsum.photos/id/11/10/6"
                max-height="200"
                max-width="500"
                src="https://picsum.photos/id/11/500/300"
              ></v-img>
              <div class="d-flex flex-row justify-space-between px-5 pt-5">
                <p class="subtitle-1 mb-0 font-weight-bold">Lorem ipsum</p>

                <v-chip>
                  <p class="body-1 mb-0 font-weight-bold">20$</p></v-chip
                >
              </div>
              <v-card-text>
                <p class="body-2 text-secondary mb-1">
                  Lorem Ipsum is simply dummy text of the printing and
                  typesetting industry.
                </p>
              </v-card-text>
              <v-divider></v-divider>
              <v-card-actions class="px-7 pb-7 pt-5">
                <v-row
                  class="d-flex flex-row align-center justify-center full-width"
                >
                  <v-btn type="submit" color="primary" block text depressed
                    ><v-icon dense class="mr-1">mdi-cart-outline</v-icon>Ajouter
                    au panier
                  </v-btn></v-row
                >
              </v-card-actions>
            </v-card>
          </v-col>
        </template>
      </div>
    </v-container>
  </v-app>
</template>

<script>
export default {
  data() {
    return {};
  },
  methods: {},
};
</script>

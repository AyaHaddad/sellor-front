<template>
  <v-app>
    <v-row>
      <v-col xl="8" lg="8" md="8" sm="12" xs="12" class="py-0">
        <v-container fluid class="py-12">
          <v-col xl="12" lg="12" md="12" sm="12" xs="12" class="py-0">
            <h4 class="display-1 mb-3 font-weight-bold">Panier</h4>
          </v-col>
          <div class="d-flex flex-row">
            <v-col xl="3" lg="3" md="3" sm="3" xs="3" class="py-0">
              <p class="body-1 text-secondary mt-3">Article</p>
            </v-col>
            <v-col xl="3" lg="3" md="3" sm="3" xs="3" class="py-0">
              <p class="body-1 text-secondary mt-3">Prix</p>
            </v-col>
            <v-col xl="3" lg="3" md="3" sm="3" xs="3" class="py-0">
              <p class="body-1 text-secondary mt-3">Quantité</p>
            </v-col>
            <v-col xl="3" lg="3" md="3" sm="3" xs="3" class="py-0">
              <p class="body-1 text-secondary mt-3">Actions</p>
            </v-col>
          </div>
          <v-divider class="mx-3 mb-3"></v-divider>
          <div v-if="products != null && products.length > 0">
            <div
              class="d-flex flex-row py-3"
              v-for="product in products"
              :key="product.id"
            >
              <v-col xl="3" lg="3" md="3" sm="3" xs="3" class="py-0">
                <p class="subtitle-1 font-weight-bold">{{ product.name }}</p>
              </v-col>
              <v-col xl="3" lg="3" md="3" sm="3" xs="3" class="py-0">
                <v-chip>
                  <p class="body-1 mb-0 font-weight-bold">
                    {{ product.price }}$
                  </p></v-chip
                >
              </v-col>
              <v-col xl="3" lg="3" md="3" sm="3" xs="3" class="py-0">
                <v-select
                  v-model="e1"
                  :items="items"
                  placeholder="quantité"
                  outlined
                  menu-props="auto"
                  dense
                  width="60px"
                ></v-select>
              </v-col>
              <v-col xl="3" lg="3" md="3" sm="3" xs="3" class="py-0">
                <v-btn type="submit" color="red" text depressed
                  ><v-icon dense class="mr-1">mdi-delete-outline</v-icon
                  >Supprimer
                </v-btn>
              </v-col>
            </div>
          </div>
        </v-container>
      </v-col>
      <v-col xl="4" lg="4" md="4" sm="12" xs="12" class="pa-0">
        <v-container
          class="pa-10 d-flex flex-row justify-center align-start fill-height"
          fluid
        >
          <v-card
            class="pa-6 m-vcard-login rounded-lg"
            height="100%"
            width="100%"
            elevation="4"
          >
            <h4 class="display-1 mb-3 font-weight-bold">Récapitulatif</h4>
            <p class="body-1 text-secondary mt-6 mb-0">Prix total</p>
            <v-divider class="my-2"></v-divider>
            <p class="subtitle-1 mb-0 font-weight-bold">20$</p>

            <v-btn
              @click="submit"
              class="mt-12"
              type="submit"
              color="primary"
              block
              depressed
              x-large
              >Commander
            </v-btn>
          </v-card>
        </v-container>
      </v-col>
    </v-row>
  </v-app>
</template>

<script>
export default {
  data() {
    return {
      myUser: {
        bucketIds: [],
      },
      products: [],
      e1: "1",
      items: ["1", "2", "3", "4"],
    };
  },

  computed: {
    test() {
      return this.$auth.strategy.token.get();
    },
  },
  mounted() {
    this.$axios
      .$get(`/auth/me`, {
        headers: {
          "Content-Type": "application/json",
          "auth-token": this.test.split(" ")[1],
        }
      })
      .then((res) => {
        console.log(res);
        this.myUser = res;
        if (this.myUser.bucketIds != null && this.myUser.bucketIds.length > 0) {
          this.myUser.bucketIds.forEach((element) => {
            console.log(element);
            this.$axios
              .$get("http://localhost:3000/products/" + element, {
                headers: {
                  "Content-Type": "application/json",
                  "auth-token": this.test.split(" ")[1],
                },
              })
              .then((response) => {
                this.products.push(response);
                console.log(response);
                console.log(this.products);
              })
              .catch((err) => console.log("err", err));
          });
        }
      })
      .catch((err) => console.log("err", err));
  },

  methods: {},
};
</script>

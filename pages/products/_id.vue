<template>
  <v-app>
    <v-container fluid class="py-12">
      <div class="d-flex flex-row">
        <v-col xl="6" lg="6" md="6" sm="12" xs="12" class="py-0">
          <v-img
            lazy-src="https://picsum.photos/id/11/10/6"
            src="https://picsum.photos/id/11/500/300"
          ></v-img
        ></v-col>
        <v-col xl="6" lg="6" md="6" sm="12" xs="12" class="pa-14">
          <h4 class="display-1 mb-3 font-weight-bold">Lorem ipsum</h4>
          <v-chip> <p class="subtitle-1 mb-0 font-weight-bold">20$</p></v-chip>
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
export default {
  data() {
    return {
      e1: "1",
      items: ["1", "2", "3", "4"],
    };
  },
  methods: {},
};
</script>

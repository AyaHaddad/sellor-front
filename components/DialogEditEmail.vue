<template>
  <v-card class="mr-0">
    <v-card-title>
      <span class="text-h5">Modifier mon Email</span>
    </v-card-title>
    <v-form ref="form">
      <v-card-text>
        <v-container>
          <v-row>
            <v-col cols="12" sm="6" md="4">
              <v-col cols="12">
                <v-text-field
                  label="Email*"
                  required
                  v-model="email"
                ></v-text-field>
              </v-col>
            </v-col>
          </v-row>
        </v-container>
      </v-card-text>
    </v-form>
    <v-card-actions>
      <v-spacer></v-spacer>
      <v-btn color="blue darken-1" text @click.stop="$emit('close-dialog')">
        Close
      </v-btn>
      <v-btn color="blue darken-1" text @click="editEmail()"> Save </v-btn>
    </v-card-actions>
  </v-card>
</template>
<script>
export default {
  name: "dialogEditEmail",

  data() {
    return {
      rules: [(v) => !!v || "Champ requis."],
      user: this.$auth.user,
      email: this.$auth.user.email,
      error: null,
    };
  },
  computed: {
    test() {
      return this.$auth.strategy.token.get();
    },
  },

  methods: {
    async editEmail() {
      if (this.$refs.form.validate()) {
        this.$axios
          .$put(
            `/users`,
            { email: this.email },
            {
              headers: {
                "Content-Type": "application/json",
                "auth-token": this.test.split(" ")[1],
              },
            }
          )
          .then(() => {
            // console.log(response);
            this.$auth.fetchUser().then((response) => {
              this.$auth.setUser(response);
            });
          });
      }
    },
  },
};
</script>

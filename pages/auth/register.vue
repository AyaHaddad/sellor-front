<template>
  <v-app>
    <div class="background-image">
      <v-container fluid class="pa-0 mt-10 pb-10 pt-15 px-3">
        <v-card class="m-vcard-login" width="550px">
          <v-card-title class="pb-0 pt-8 text-center">
            S'inscrire
          </v-card-title>

          <v-form
            class="m-vform-login"
            method="post"
            @submit.prevent="submit"
            ref="form"
          >
            <v-card-text class="py-7 px-3 pa-sm-7 pa-md-7 pa-lg-7 pa-xl-7 pb-0">
              <!-- column genre -->
              <v-row justify="center">
                <v-col cols="11" xl="7" lg="7" md="7" sm="7" class="py-0">
                  <v-text-field
                    v-model="email"
                    label="Email"
                    type="email"
                    :rules="rules"
                    outlined
                  ></v-text-field>
                </v-col>
              </v-row>
              <v-row justify="center">
                <v-col cols="11" xl="7" lg="7" md="7" sm="7" class="py-0">
                  <v-text-field
                    v-model="name"
                    label="Pseudo"
                    :rules="rules"
                    outlined
                  ></v-text-field>
                </v-col>
              </v-row>
              <!-- column respons -->
              <v-row justify="center">
                <v-col cols="11" xl="7" lg="7" md="7" sm="7" class="py-0">
                  <v-text-field
                    v-model="password"
                    label="Mot de passe"
                    :rules="rules_password"
                    outlined
                  ></v-text-field>
                </v-col>
              </v-row>
            </v-card-text>
            <v-card-actions class="pa-5">
              <v-row
                class="d-flex flex-row align-center justify-center full-width"
              >
                <v-btn type="submit" class="m-button m-primary" text>
                  <span class="v-btn-content">Se connecter</span>
                </v-btn>
              </v-row>
            </v-card-actions>
          </v-form>
        </v-card>
      </v-container>
    </div>
  </v-app>
</template>

<script>
export default {
  name: "register",
  auth: "guest",
  data() {
    return {
      name: "",
      email: "",
      password: "",
      rules: [(v) => !!v || "Champ requis."],
      rules_password: [
        (v) => !!v || "Champ requis.",
        (v) =>
          v.length >= 6 ||
          "Le mot de passe doit être composé de 6 caractères minimun !",
      ],
    };
  },
  methods: {
    async submit() {
      if (this.$refs.form.validate()) {
        await fetch("http://localhost:3000/auth/register", {
          method: "POST",
          headers: { "Content-Type": "application/json" },
          body: JSON.stringify({
            name: this.name,
            email: this.email,
            password: this.password,
          }),
        });
        await this.$router.push("login");
      }
    },
  },
};
</script>

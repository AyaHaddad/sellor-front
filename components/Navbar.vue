<template>
  <v-app-bar
    app
    class="mainToolbar"
    elevation="0"
    color="primary"
    height="60"
    dense
  >
    <nuxt-link to="/">
      <v-toolbar-title>Sellor</v-toolbar-title>
    </nuxt-link>

    <v-spacer></v-spacer>
    <v-menu v-if="$auth.loggedIn">
      <template v-slot:activator="{ on, attrs }">
        <!--username-->
        <v-btn elevation="0" :ripple="false" v-bind="attrs" v-on="on">
          {{ email }}
          <v-icon class="pl-3" color="000">mdi-triangle-small-down</v-icon>
        </v-btn>

        <!--basket-->
        <v-btn @click="$auth.logout()"> Déconnexion </v-btn>
      </template>
      <v-list class="m-vlist-dropdown">
        <v-divider></v-divider>
        <v-list-item @click="openEditEmail = true">
          <v-list-item-title cols="auto">Editer mon email</v-list-item-title>
          <v-icon cols="auto" color="#001D46">fa-envelope</v-icon>
        </v-list-item>

        <v-divider></v-divider>
        <v-list-item @click="openEditPassword = true">
          <v-list-item-title cols="auto"
            >Editer mon mot de passe</v-list-item-title
          >
          <v-icon cols="auto" color="#001D46">fa-lock</v-icon>
        </v-list-item>
        <v-divider></v-divider>

        <!-- <v-divider></v-divider>
        <v-list-item @click="logout">
          <v-list-item-title cols="auto">Se déconnecter</v-list-item-title>
          <v-icon cols="auto" color="#001D46">fa-sign-out-alt</v-icon>
        </v-list-item> -->
      </v-list>
    </v-menu>

    <div v-else>
      <v-btn color="white" outlined depressed to="/auth/login" nuxt
        >Se connecter</v-btn
      >
      <v-btn color="white" text depressed to="/auth/register" nuxt
        >S'inscrire</v-btn
      >
    </div>
    <v-dialog v-model="openEditEmail">
      <dialog-edit-email
        v-on:close-dialog="openEditEmail = false"
      ></dialog-edit-email>
    </v-dialog>

    <v-dialog v-model="openEditPassword">
      <dialog-edit-password
        v-on:close-dialog="openEditPassword = false"
      ></dialog-edit-password>
    </v-dialog>
  </v-app-bar>
</template>

<script>
export default {
  data() {
    return {
      openEditEmail: false,
      openEditPassword: false,
    };
  },
  computed: {
    email() {
      return this.$auth.user;
    },
  },
};
</script>

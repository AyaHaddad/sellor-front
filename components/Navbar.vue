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
    <div v-if="$auth.loggedIn">
      <!--username-->
      {{ $auth.user.email }}
      <!--basket-->
      <v-btn @click="$auth.logout()"> Déconnexion </v-btn>
    </div>
    <div v-else>
      <v-btn color="white" outlined depressed to="/auth/login" nuxt
        >Se connecter</v-btn
      >
      <v-btn color="white" text depressed to="/auth/register" nuxt
        >S'inscrire</v-btn
      >
    </div>
  </v-app-bar>
</template>

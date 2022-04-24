<template>
  <v-app-bar
    app
    class="mainToolbar"
    elevation="0"
    color="primary"
    height="60"
    dense
  >
    <v-toolbar-title>Sellor</v-toolbar-title>

    <v-spacer></v-spacer>
    <div v-if="$auth.loggedIn">
      <!--username-->
      {{ $auth.user.email }}
      <!--basket-->
      <v-btn> Déconnexion </v-btn>
    </div>
    <div v-else>
      <v-btn color="white" outlined depressed to="auth/login"
        >Se connecter</v-btn
      >
      <v-btn color="white" text depressed to="auth/register">S'inscrire</v-btn>
    </div>
  </v-app-bar>
</template>

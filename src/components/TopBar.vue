<template>
    <div>
      <v-toolbar
        dark
        prominent
        src="https://cdn.vuetifyjs.com/images/backgrounds/vbanner.jpg"
      >
       
        <v-spacer></v-spacer>
  
        <v-btn icon @click="showLogoutDialog = true">
        <v-icon>mdi-export</v-icon>
        </v-btn>

        <v-dialog v-model="showLogoutDialog"  max-width="50vw">
      <v-card class="d-flex align-self-center">
        <v-card-title class="headline">Cerrar sesión</v-card-title>
        <v-card-text>" "</v-card-text>

        <v-card-actions>
          <v-btn text @click="showLogoutDialog = false">Cancelar</v-btn>
          <v-btn color="primary" text @click="logout">Aceptar</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>

      </v-toolbar>
    </div>
  </template>

<script>
import { getAuth, signOut } from "firebase/auth";

export default {
  data: () => ({
    showLogoutDialog: false,
  }),

  methods: {
    async logout() {
      try {
        const auth = getAuth();
        await signOut(auth);
        console.log('Sesión cerrada');
        this.$router.push('/');
      } catch (err) {
        console.error(err.message);
      }
    },
  },
};
</script>
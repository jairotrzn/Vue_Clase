<template>
  <v-app>

    <TopBar/>
    <SideBar/>

    <v-container>
      <v-row>
        <v-col cols="12" sm="9">
          <v-row>
            <v-col cols="12" sm="12">
              <h1>Formulario</h1>
            </v-col>
            <v-col cols="12" sm="11">
              <Tabla/>
            </v-col>
          </v-row>
        </v-col>
        <v-col cols="12" sm="3">
        
        </v-col>
      </v-row>
    </v-container>
  </v-app>
   
</template>

<script>
  
  import SideBar from '@/components/SideBar.vue'
  import TopBar from '@/components/TopBar.vue'
  import Tabla from '@/components/Tabla.vue'
  export default {
    name: 'Home',

    components: {
      TopBar,
      SideBar,
      Tabla
    },
  }
</script>

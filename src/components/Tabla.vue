<template>
  <v-card>
    <v-card-title>
      <v-text-field
        v-model="search"
        append-icon="mdi-magnify"
        label="Search"
        single-line
        hide-details
      ></v-text-field>
      <template>
        <div class="text-center">
          <v-btn
            class="mx-2"
            fab
            dark
            color="indigo"
            @click="dialogoCreate = true"
          >
            <v-icon dark>mdi-plus</v-icon>
          </v-btn>
        </div>
      </template>
    </v-card-title>
    <v-data-table
      :headers="headers"
      :items="users"
      :search="search"
    >
    <template v-slot:item.actions="{ item }">
        <v-icon small class="mr-2" color="red" @click="deleteMachine(item)"
          >mdi-delete</v-icon
        >
        <v-icon
          small
          color="blue"
          @click="
            selectedMachine = item;
            dialogUpdate = true;
          "
          >mdi-pencil</v-icon
        >
      </template>

  </v-data-table>

    <v-dialog v-model="dialogoCreate">
      <v-card>
        <v-container>
          <v-form @submit.prevent="addPerson">
            <p><b>Formulario personas</b></p>
            <v-text-field
              type="text"
              label="Agregar Nombre"
              v-model="name"
            >
            </v-text-field>
            <v-text-field
              type="email"
              label="Agregar email"
              v-model="email"
            >
            </v-text-field>

            <v-text-field
              type="text"
              label="Agregar Direccion"
              v-model="adress"
            >
            </v-text-field>

            <v-text-field
              type="date"
              label="Agregar fecha de nacimiento"
              v-model="age"
            >
            </v-text-field>
            <v-btn
              type="submit"
              color="primary"
              class="mr-4"
              @click.stop="dialogoCreate = false"
              >Agregar</v-btn
            >
          </v-form>
        </v-container>
      </v-card>
    </v-dialog>
  </v-card>
</template>

<script>

import { db, collection, getDocs, addDoc, deleteDoc, doc,updateDoc } from "../Config/firebase";
export default {
  data() {
    return {
      search: "",
      dialogoCreate: false,
      name: "",
      email: "",
      adress: "",
      age: 0,
    
      users:[],
      
      headers: [
        { text: "Nombre", value: "name" },
        { text: "Email", value: "email" },
        { text: "Direccion", value: "adress" },
        { text: "Edad", value: "age" },
        { text: "Acciones", value: "actions" },
      ],

    };

  },
  created() {
    this.getUsers();
  },
     methods:{
        async getUsers(){
          
            try {
                
                const usersDb = await getDocs(collection(db,"coleccionPrueba"));

                const users = [];

                usersDb.forEach((doc) =>{
                    let usersData = doc.data();
                    usersData.id = doc.id;
                    users.push(usersData);
                });
                this.users = users;
            } catch (error) {
                console.log(error)
            }
        },

        async addPerson(){

            try {
                await addDoc(collection(db,"coleccionPrueba"),{
                name:this.name,
                email:this.email,
                adress:this.adress,
                age:this.age
            })
            } catch (error) {
                console.log(error)
            }
            this.getUsers();
           
        }
    }
};
</script>

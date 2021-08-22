<template>
  <v-row justify="center">
    <v-dialog
      :value="showModal"
      persistent
      max-width="600px"
    >
      <v-card>
        <v-card-title>
          <span class="text-h5">Registro de Nuevos Usuarios</span>
        </v-card-title>
        <v-card-text>
          <v-container>
            <v-row>
              <v-col
                cols="12"
                sm="6"
                md="4"
              >
                <v-text-field
                  label="Rut"
                  required
                ></v-text-field>
              </v-col>
            </v-row>
            <v-row>
              <v-col
                cols="12"
                sm="6"
                md="4"
              >
                <v-text-field
                  label="Ingrese Contraseña"
                  required
                ></v-text-field>
              </v-col>
            </v-row>
            <v-row>
              <v-col
                cols="12"
                sm="6"
                md="4"
              >
                <v-text-field
                  label="Reingrese la Contraseña"
                  required
                ></v-text-field>
              </v-col>
            </v-row>
          </v-container>
          <small class="red--text">Todos los campos son obligatorios</small>
        </v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn
            color="blue darken-1"
            text
            @click="sendModal()"
          >
            Cerrar
          </v-btn>
          <v-btn
            color="blue darken-1"
            text
            @click="sendModal()"
          >
            Guardar
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-row>
</template>

<script>
  export default {
    name: 'CrearCuenta',
    props : [
        'showModal',
    ],
    data: () => ({
      dialog: false,
    }),
    methods:{
        sendModal(){
            // this.showModal = false;
            // const verModal = false;
            this.$emit('verModal', false);
        }
    }
  }
</script>
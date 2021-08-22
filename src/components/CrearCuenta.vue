<template>
    <ValidationObserver ref="observer">
        <v-row justify="center">
        <v-dialog
            :value="showModal"
            persistent
            max-width="600px"
        >
            <v-card>
            <v-card-title>
                <span class="text-h5 font-weight-bold blue--text">Registro de Nuevos Usuarios</span>
            </v-card-title>
            <v-card-text>
                <v-container>
                <v-row>
                    <v-col
                        cols="10"
                    >
                        <ValidationProvider v-slot="{ errors }" rules="required|rut">
                            <v-text-field
                                label="Rut"
                                required
                                v-model="rut"
                                name="user[rutDirective]" 
                                v-rutDirective:live
                                :error-messages="errors"
                            ></v-text-field>
                        </ValidationProvider>
                    </v-col>
                </v-row>
                <v-row>
                    <v-col
                    cols="10"
                    >
                    <ValidationProvider v-slot="{ errors }" rules="required|minMaxPass:4,30">
                        <v-text-field
                            label="Ingrese Contraseña"
                            required
                            :error-messages="errors"
                            v-model="pass"
                            :append-icon="showPassword ? 'mdi-eye' : 'mdi-eye-off'"
                            @click:append="showPassword = !showPassword"
                            :type="showPassword ? 'text' : 'password'" 
                        ></v-text-field>
                    </ValidationProvider>
                    </v-col>
                </v-row>
                <v-row>
                    <v-col
                    cols="10"
                    >
                    <ValidationProvider v-slot="{ errors }" rules="required|minMaxPass:4,30">
                        <v-text-field
                            label="Repita Contraseña"
                            required
                            :error-messages="errors"
                            v-model="otherPass"
                            :append-icon="showOtherPassword ? 'mdi-eye' : 'mdi-eye-off'"
                            @click:append="showOtherPassword = !showOtherPassword"
                            :type="showOtherPassword ? 'text' : 'password'"
                        ></v-text-field>
                    </ValidationProvider>
                    </v-col>
                </v-row>
                </v-container>
                <small class="red--text font-weight-bold">Todos los campos son obligatorios</small>
            </v-card-text>
            <v-card-actions>
                <v-spacer></v-spacer>
                <v-btn
                color="red darken-1"
                class="white--text"
                @click="sendModal()"
                >
                Cerrar
                </v-btn>
                <v-btn
                color="blue darken-1"
                @click="sendModal()"
                class="white--text"
                >
                Guardar
                </v-btn>
            </v-card-actions>
            </v-card>
        </v-dialog>
        </v-row>
    </ValidationObserver>
</template>

<script>
    import {rutValidator, rutInputDirective } from "vue-dni";
    import { ValidationObserver, ValidationProvider,extend } from "vee-validate";
    import { required } from 'vee-validate/dist/rules';
    import Vue from 'vue';

    Vue.directive('rutDirective', rutInputDirective);

    extend('required', {
        ...required,
        message: 'Este campo es obligatorio'
    });

    extend("rut", {
        computesRequired: true,
        validate: value => !!rutValidator(value),
        message: "Debe ingresar un rut válido"
    });

    extend('minMaxPass', {
        validate(value, {min, max}){
            const largoPass = value.length;
            return Number(largoPass) >= Number(min) && Number(largoPass) <= Number(max);
        },
        params:['min', 'max'],
        message: 'Debe ingresar una contraseña entre 4 y 30 caracteres'
    })

    export default {
        components:{   
            ValidationProvider,
            ValidationObserver,
        },
        name: 'CrearCuenta',
        props : [
            'showModal',
        ],
        data: () => ({
            rut: '',
            pass:'',
            otherPass:'',
            showPassword:false,
            showOtherPassword:false,
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
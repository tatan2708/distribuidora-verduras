<template>
    <ValidationObserver ref="observer">
        <div class="fondo-auth">
            <v-row class="purple darken-4">
                <v-col class="titulo-auth">
                    Gestor de la distribuidora y productora de verduras Beas    
                </v-col>
            </v-row>
            <v-row>
                <v-col class="card-auth">
                    <div>
                        <v-card width="400" class="mx-auto pa-4">
                            <v-card-title class="pb-0">
                                <h1>Login</h1>
                            </v-card-title>
                            <v-spacer></v-spacer>
                            <v-card-text>
                                <v-form>
                                    <ValidationProvider v-slot="{ errors }" rules="required|rut">
                                        <v-text-field 
                                            label="Rut" 
                                            prepend-icon="mdi-account-circle"
                                            :error-messages="errors"
                                            v-model="rut"
                                            name="user[rutDirective]" 
                                            v-rutDirective:live
                                        />
                                    </ValidationProvider>
                                    <ValidationProvider v-slot="{ errors }" 
                                        rules="required"
                                    >
                                        <v-text-field
                                            label="Contraseña"
                                            prepend-icon="mdi-lock"
                                            :error-messages="errors"
                                            v-model="pass"
                                            :append-icon="showPassword ? 'mdi-eye' : 'mdi-eye-off'"
                                            @click:append="showPassword = !showPassword"
                                            :type="showPassword ? 'text' : 'password'" 
                                        />
                                    </ValidationProvider>
                                </v-form>
                            </v-card-text>
                            <v-divider></v-divider>
                            <v-card-actions class="pt-3">
                                <v-btn color="info">Acceder</v-btn>
                                <v-btn 
                                    color="success"
                                    @click="showModal = true"
                                >
                                    Crear Cuenta
                                </v-btn>
                            </v-card-actions>
                        </v-card>

                        <CrearCuenta
                            :showModal="showModal"
                            @verModal = "getValueShow"
                        />
                    </div>
                </v-col>
            </v-row>
        </div>
    </ValidationObserver>
</template>

<style scoped>
    .titulo-auth{
        font-size: 30px;
        font-weight: bold;
        padding: 30px 0 30px 40px;
        color: white;
    }
    .fondo-auth{
        background-image: url('../assets/pexels-magda-ehlers-1300972.jpg');
        overflow: hidden;
        background-size: cover;
        width: 100%;
        min-height: 100vh;
    }
    .card-auth{
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        height: calc(100vh - 110px);
        
    }
</style>

<script>
    import {rutValidator, rutInputDirective } from "vue-dni";
    import { ValidationObserver, ValidationProvider,extend } from "vee-validate";
    import { required } from 'vee-validate/dist/rules';
    import Vue from 'vue';
    import CrearCuenta from '@/components/CrearCuenta.vue';

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

    export default({
        components:{   
            ValidationProvider,
            ValidationObserver,
            CrearCuenta
        },
        data: () => ({
            rut: '',
            pass:'',
            showPassword:false,
            showModal: false,
        }),
        methods:{
            getValueShow(value){
                this.showModal = value;
            },
        }
    })
</script>

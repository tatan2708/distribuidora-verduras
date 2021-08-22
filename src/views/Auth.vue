<template>
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
                            <v-text-field 
                                label="Rut" 
                                prepend-icon="mdi-account-circle"
                            />
                            <v-text-field 
                                :type="showPassword ? 'text' : 'password'" 
                                label="Contraseña"
                                prepend-icon="mdi-lock"
                                :append-icon="showPassword ? 'mdi-eye' : 'mdi-eye-off'"
                                @click:append="showPassword = !showPassword"
                            />
                            </v-form>
                        </v-card-text>
                        <v-divider></v-divider>
                        <v-card-actions class="pt-3">
                            <v-btn color="info">Acceder</v-btn>
                            <v-btn color="success">Crear Cuenta</v-btn>
                        </v-card-actions>
                    </v-card>
                </div>
            </v-col>
        </v-row>
    </div>
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
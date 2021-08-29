<template>
    <ValidationObserver 
        ref="observer"
    >
        <div>
            <v-container>
                <v-row class="text-center">
                    <v-col>
                        <h1>Productos Disponibles</h1>
                    </v-col>
                </v-row>
                <v-row class="pb-6">
                    <v-col cols="6">
                        <ul>
                            <li>Papa $14000 el saco </li>
                            <li>Cebollas $20000 el saco </li>
                        </ul>
                        <!-- <div>
                            <p>Papa $4000 el saco </p>
                        </div>
                        <div>
                            <p>Papa $4000 el saco </p>
                        </div> -->
                    </v-col>
                    <v-col cols="6">
                        <ul>
                            <li>Betarragas $10000 el saco </li>
                            <li>Zanahorias $20000 el saco </li>
                        </ul>
                        <!-- <div>
                            <p>Papa $4000 el saco </p>
                        </div>
                        <div>
                            <p>Papa $4000 el saco </p>
                        </div> -->
                    </v-col>
                </v-row>
                <v-divider></v-divider>
                <v-row class="my-10">
                    <v-card
                        class="mx-auto"
                    >
                        <v-card-title class="text-h5 font-weight-bold">
                            Pedidos
                        </v-card-title>

                        <v-divider></v-divider>

                        <v-card-text>
                            <v-list three-line>
                                <template v-for="(item, index) in items">
                                    <v-subheader
                                        v-if="item.header"
                                        :key="item.header"
                                        v-text="item.header"
                                    ></v-subheader>

                                    <v-divider
                                        v-else-if="item.divider"
                                        :key="index"
                                        :inset="item.inset"
                                    ></v-divider>

                                    <v-list-item
                                    v-else
                                    :key="item.title"
                                    >
                                    <v-list-item-avatar>
                                        <v-img :src="item.avatar"></v-img>
                                    </v-list-item-avatar>

                                    <v-list-item-content>
                                        <v-list-item-title v-html="item.title"></v-list-item-title>
                                        <v-list-item-subtitle>{{item.cantidad}} sacos</v-list-item-subtitle>
                                        <v-list-item-subtitle>Total: ${{item.precio*item.cantidad}}</v-list-item-subtitle>
                                    </v-list-item-content>
                                    </v-list-item>
                                    
                                </template>

                            </v-list>
                        </v-card-text>

                        <v-card-actions>
                            <v-col class="text-right">
                                <v-btn
                                    class="mx-2 text-center"
                                    fab
                                    dark
                                    color="indigo"
                                    @click="isModal = true"
                                >
                                    <v-icon dark>
                                        mdi-plus
                                    </v-icon>
                                </v-btn>
                            </v-col>
                        </v-card-actions>

                    </v-card>
                </v-row>
                <v-row>
                    <v-dialog
                        :value="isModal"
                        persistent
                        max-width="600px"
                    >
                        <v-card>
                            <v-card-title>
                                <span class="text-h5 font-weight-bold purple--text">Ingreso Pedidos</span>
                            </v-card-title>
                            <v-card-text>
                                <v-container>
                                    <v-form
                                        ref="form"
                                        lazy-validation
                                    >
                                        <v-row>
                                        <v-text-field
                                            label="Rut"
                                            required
                                            v-model="rut"
                                            @blur="formatRut($event.target.value)" 
                                            v-rutDirective:live
                                            :error-messages="errors"
                                        ></v-text-field>

                                        </v-row>
                                    </v-form>
                                </v-container>
                            </v-card-text>
                        </v-card>
                    </v-dialog>
                </v-row>

            </v-container>
        </div>
    </ValidationObserver>
</template>

<script>
    import { ValidationObserver, ValidationProvider,extend } from "vee-validate";
    import { required } from 'vee-validate/dist/rules';

    extend('required', {
        ...required,
        message: 'Este campo es obligatorio'
    });

    export default({
        components:{   
            ValidationProvider,
            ValidationObserver,
        },
        data: () => ({
            isModal: false,
            pedidos:[
                {
                    producto:'papas',
                    precio: 14000,
                    cantidad: 5,
                },
                {
                    producto:'cebolla',
                    precio: 14000,
                    cantidad: 3,
                },
                {
                    producto:'betarraga',
                    precio: 14000,
                    cantidad: 2,
                },
                {
                    producto:'zahahora',
                    precio: 14000,
                    cantidad: 6,
                },
            ],

            items: [
                {
                    avatar: require('../assets/papas.jpeg'),
                    title: 'Papas',
                    cantidad: 6,
                    precio: 14000,
                },
                { divider: true, inset: true },
                {
                    avatar: require('../assets/betarragas.jpeg'),
                    title: 'Betarragas',
                    cantidad: 4,
                    precio: 10000,
                },
                { divider: true, inset: true },
                {
                    avatar: require('../assets/zanahorias.webp'),
                    title: 'Zanahorias',
                    cantidad: 3,
                    precio: 20000,
                },
                { divider: true, inset: true },
                {
                    avatar: require('../assets/cebollas.jpeg'),
                    title: 'Cebollas',
                    cantidad: 4,
                    precio: 20000,
                },
            ],
        }),
    })
</script>

<style scoped>


</style>

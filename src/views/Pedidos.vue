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
                                        <template v-if="numberItem > 0">
                                            <template v-for="(i) in numberItem">
                                                <v-row :key="i" v-if="numberItem > 0">
                                                        <v-col cols="5">
                                                            <ValidationProvider v-slot="{ errors }" rules="required">
                                                                <v-select
                                                                    :items="verduras"
                                                                    :error-messages="errors"
                                                                    label="Verduras"
                                                                    item-text="nombre"
                                                                    item-value="id"
                                                                    v-model="id"
                                                                ></v-select>
                                                            </ValidationProvider>                                               
                                                        </v-col>
                                                        <v-col cols="5">
                                                            <ValidationProvider v-slot="{ errors }" rules="required">
                                                                <v-text-field
                                                                    :items="verduras"
                                                                    label="Cantidad"
                                                                    required
                                                                    :error-messages="errors"
                                                                    type="number"
                                                                    :min=1
                                                                    item-text="nombre"
                                                                    item-value="id"
                                                                    v-model="cantidad"
                                                                ></v-text-field>
                                                            </ValidationProvider>                                               
                                                        </v-col>
                                                </v-row>
                                            </template>
                                        </template>
                                        <v-row class="textDefault py-6 pb-0" v-else>
                                            <div>
                                                Ingrese un pedido
                                            </div>
                                        </v-row>
                                    </v-form>
                                </v-container>
                            </v-card-text>

                            <v-card-actions>
                                <v-col class="text-left">
                                    <v-btn
                                        class="mx-2 text-center"
                                        dark
                                        color="red"
                                        @click="isModal=false"
                                    >
                                        Cerrar
                                    </v-btn>
                                </v-col>
                                <v-col class="text-center">
                                    <v-btn
                                        class="mx-2 text-center"
                                        dark
                                        color="blue"
                                        @click="isModal=false"
                                    >
                                        Enviar
                                    </v-btn>
                                </v-col>
                                <v-col class="text-right">
                                    <v-btn
                                        class="mx-2 text-center"
                                        fab
                                        color="indigo"
                                        @click="addRow()"
                                        :disabled="addDisabled || disabledBtn"
                                    >
                                        <v-icon dark>
                                            mdi-plus
                                        </v-icon>
                                    </v-btn>
                                </v-col>
                            </v-card-actions>
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
            id:null,
            cantidad:null,
            listoId:false,
            listoCantidad:false,
            addDisabled: false,
            itemAddSDynamic:[],
            numberItem: 0,
            addPedidos:[],
            isModal: false,
            verduras:[
                {   
                    id: 1,
                    nombre: 'Papas'
                },
                {   
                    id: 2,
                    nombre: 'Zanahorias'
                },
                {   
                    id: 3,
                    nombre: 'Betarragas'
                },
                {   
                    id: 4,
                    nombre: 'Cebollas'
                },
            ],
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
        methods:{
            addRow(){
                this.addDisabled = true;
                this.numberItem += 1;
                const objectVerduras = {
                    id: this.id,
                    cantidad: this.cantidad
                }
                if(this.id != null){
                    this.itemAddSDynamic.push(objectVerduras);
                }
            },
        },
        watch: {
            id(val){
                this.id = val;
                if(this.id != null){
                    this.listoId = true;
                }
            },
            cantidad(val){
                this.cantidad = val;
                if(this.cantidad != null){ 
                    this.addDisabled = false;
                }
            },
        },
        computed:{
            disabledBtn(){
                if(this.listoCantidad && this.listoId){
                    return true;
                }
                return false;
            }
        }
    })
</script>

<style scoped>
    .textDefault{
        display: flex;
        flex-direction: row;
        align-items: center;
        justify-content: center;
        font-size: 20px;
    }
</style>

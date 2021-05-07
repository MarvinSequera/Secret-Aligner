<template>
    <v-row justify="center">
        <v-dialog
            v-if="openDetail"
            v-model="openDetail"
            max-width="800px"
            @click:outside="close"
        >
            <v-card id="print"  class="px-8">
                <v-row>
                    <v-col class="text-center">
                        <v-icon color="black" size="300px">mdi-account</v-icon>
                    </v-col>
                    <v-divider vertical></v-divider>
                    <v-col>
                        <div>
                            <span class="text-h4">{{ user.ficha_dental.clinica }}</span>
                        </div>
                        <v-divider></v-divider>
                        <div>
                            <span class="text-h4">{{ user.datos_paciente.nombre }}</span>
                        </div>
                        <v-divider></v-divider>
                        <div>
                            <span class="text-h4">{{ user.datos_paciente.apellidos }}</span>
                        </div>
                        <v-divider></v-divider>
                        <div>
                            <span class="text-h4 mr-4">{{ user.datos_paciente.sexo}}</span>
                            <v-divider vertical></v-divider>
                            <span class="text-h4">{{ user.datos_paciente.fecha_nacimiento }}</span>
                        </div>
                    </v-col>
                </v-row>
                <v-divider></v-divider>
                <v-row>
                    <v-col>
                        <span class="text-h4">Dientes No Mover</span>
                    </v-col>
                    <v-divider vertical></v-divider>
                    <v-col>

                    </v-col>
                </v-row>
                <v-divider></v-divider>
                <v-row>
                    <v-col>
                        <v-img
                            :src="maxilar"
                            width="349px"
                        >
                        </v-img>
                    </v-col>
                    <v-divider vertical></v-divider>
                    <v-col>
                        <div>
                            <span class="text-h4">{{ user.ficha_dental.estado.toUpperCase() }}</span>
                        </div>
                        <v-divider></v-divider>
                        <div>
                            <span class="text-h4">{{ user.ficha_dental.objetivo_tratamiento }}</span>
                        </div>
                        <v-divider></v-divider>
                        <div>
                            <span class="text-h4">Recorte de Alineadores</span>
                        </div>
                        <div class="pb-2">
                            <span class="text-h5">{{ user.ficha_dental.otros_datos.recorte_alineadores }}</span>
                        </div>
                        <div>
                            <span class="text-h4">¿Desea alineadores pasivos?</span>
                        </div>
                        <div class="pb-2">
                            <span class="text-h5">{{ user.ficha_dental.otros_datos.alineadores_pasivos ? 'Si' : 'No' }}</span>
                        </div>
                        <div>
                            <span class="text-h4">¿Desea SecretRetainer al finalizar?</span>
                        </div>
                        <div>
                            <span class="text-h5">{{ user.ficha_dental.otros_datos.secretretainer ? 'Si' : 'No' }}</span>
                        </div>
                    </v-col>
                </v-row>
                <v-card-actions class="pb-8">
                    <v-btn
                        color="blue"
                    >
                        Descarga PDF
                    </v-btn>
                </v-card-actions>
            </v-card>
        </v-dialog>
    </v-row>
</template>

<script>
import maxilar from '../../assets/maxilar.jpg'

export default {
    model: {
        prop: 'openDetail',
        event: 'change'
    }, 
    props: {
        openDetail: {
            required: true,
            type: Boolean
        },
        user: {
            requied: true,
            type: Object
        }
    },
    data: () => ({
        maxilar
    }),
    methods: {
        close() {
            this.$emit('change', false)
        }
    },
}
</script>

<style lang="scss" scoped>

</style>

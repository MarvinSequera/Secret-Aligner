<template>
    <v-row justify="center">
        <v-dialog
            v-model="openDialog"
            max-width="800px"
            @click:outside="close"
        >
            <v-card class="px-16">
                <v-card-title class="d-flex justify-center my-4">
                    <span class="text-h4">Dar de Alta</span>
                </v-card-title>
                <v-form
                    ref="form"
                >
                    <v-row>
                        <v-text-field
                            label="Nombre"
                            solo
                            v-model.trim="patient.name"
                        />
                    </v-row>
                    <v-row>
                        <v-text-field
                            label="Apellidos"
                            solo
                            v-model.trim="patient.surName"
                        />
                    </v-row>
                    <v-row>
                        <v-col
                            cols="6"                        
                        >
                            <span>Cumpleaños</span>
                            <v-date-picker
                                v-model="patient.birthDate"
                                :first-day-of-week="1"
                                locale="es-es"
                            />
                        </v-col>

                        <v-col
                            cols="6"
                        >
                            <v-select
                                class="mt-6"
                                label="Sexo"
                                :items="sexOptions"
                                outlined
                                v-model="patient.sex"
                            />

                            <v-text-field
                                label="Clinica"
                                solo
                                v-model.trim="patient.clinic"
                            />

                            <v-select
                                label="Objetivo del tratamiento"
                                :items="treatmentOptions"
                                outlined
                                v-model="patient.treatment"
                            />
                        </v-col>
                    </v-row>
                    <v-row>
                        <v-col
                            cols="6"
                        >
                            <v-radio-group
                                label="Recorte Alineadores"
                                v-model="patient.alignersCut"
                            >
                                <v-radio
                                    v-for="n in 2"
                                    :key="n"
                                    :value="treatment[n-1]"
                                    :label="treatment[n-1]"
                                >

                                </v-radio>
                            </v-radio-group>
                        </v-col>
                        <v-col
                            cols="3"
                        >
                            <v-radio-group
                                label="¿Alineadores pasivos?"
                                v-model="patient.pasiveAligners"
                            >
                                <v-radio
                                    v-for="n in 2"
                                    :key="n"
                                    :value="checkBox[n-1]"
                                    :label="checkBox[n-1]"
                                >

                                </v-radio>
                            </v-radio-group>
                        </v-col>
                        <v-col
                            cols="3"
                        >
                            <v-radio-group
                                label="¿SecretRetrainer?"
                                v-model="patient.secretRetrainer"
                            >
                                <v-radio
                                    v-for="n in 2"
                                    :key="n"
                                    :value="checkBox[n-1]"
                                    :label="checkBox[n-1]"
                                >

                                </v-radio>
                            </v-radio-group>
                        </v-col>
                    </v-row>
                </v-form>
                <v-card-actions
                    class="pb-8 d-flex justify-end"
                >
                    <v-btn
                        color="info"
                        @click="reset"
                    >
                        Limpiar
                    </v-btn>
                    <v-btn
                        color="error"
                        @click="close"
                    >
                        Cancelar
                    </v-btn>
                    <v-btn
                        color="success"
                        :loading="loading"
                        @click="fakeAjax"
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
    model: {
        prop: 'openDialog',
        event: 'change'
    },
    props: {
        openDialog: {
            required: true,
            type: Boolean
        }
    },
    data: () => ({
        patient: {
            name: '',
            surName: '',
            birthDate: new Date().toISOString().substr(0, 10),
            sex: undefined,
            clinic: '',
            treatment: undefined,
            alignersCut: undefined,
            pasiveAligners: undefined,
            secretRetrainer: undefined,
        },
        sexOptions: ['Masculino', 'Femenino'],
        treatmentOptions: ['Estética', 'Oclusión', 'Estética y Oclusión'],
        checkBox: ['Si', 'No'],
        treatment: ['Recortar dejando 1-3 mm de encía', 'Recortar a nivel de los cuellos'],
        loading: false
    }),
    methods: {
        close() {
            this.$emit('change', false)
        },
        radioButtom(value, input) {
            this.patient[input] = value
        },
        reset () {
            this.$refs.form.reset()
        },
        fakeAjax() {
            this.loading = true
            console.log(this.patient)
            setTimeout(() => this.loading = false, 5000 )
        }
    },
}
</script>

<style lang="scss" scoped>

</style>

<template>
    <v-container class="ma-0 px-0 pb-0 av-body av-container">
        <v-row 
            class="av-body"
            dense
        >
            <v-col cols="2" class="av-middle-shadow px-0">
            </v-col>
            <v-col cols="10">
                <SubHeader/>
                <v-row class="pt-4" >
                    <v-col
                        cols="3"
                    >
                        <v-row>
                            <v-col 
                                cols="2"
                                align-self="center"
                            >
                                <v-icon 
                                    size="30px"
                                    class="pl-4"
                                    color="black"
                                >
                                    mdi-card-account-details-outline
                                </v-icon>
                            </v-col>
                            <v-col 
                                cols="8"
                                align-self="center"
                            >
                                <span class="text-h5">
                                    Listado de Pacientes
                                </span>
                                <span class="text-body-2 font-weight-light">
                                    Visualización de pacientes
                                </span>
                            </v-col>
                        </v-row>
                    </v-col>
                    <v-spacer/>
                    <v-col
                        cols="5"
                    >
                        <v-text-field
                            solo
                            flat
                            placeholder=" Buscar"
                            prepend-inner-icon="mdi-magnify"
                            background-color="#EDEDED"
                            v-model="searchByName"
                        />
                    </v-col>
                    <v-col cols="1"/>
                </v-row>
                <v-row dense>
                    <v-col>
                        <v-btn
                            outlined
                            color="#2D82D7"
                            class="py-6 mx-4"
                            width="200"
                        >
                            <v-icon class="pr-2">mdi-plus</v-icon>
                            <span class="text-subtitle-1">
                                Nuevo Paciente
                            </span>
                        </v-btn>
                        <v-btn
                            outlined
                            color="#2D82D7"
                            class="py-6"
                            width="200"
                            @click="createCSV"
                        >
                            <v-icon class="pr-2">mdi-file-download</v-icon>
                            <span class="text-subtitle-1">
                                Descargar CSV                        
                            </span> 
                        </v-btn>
                    </v-col>
                </v-row>
                <v-row>
                    <v-col>
                        <v-icon 
                            size="30px"
                            class="pl-4"
                            color="black"
                            @click="changeDisplay(false)"
                        >
                            mdi-menu
                        </v-icon>
                        <v-icon 
                            size="30px"
                            class="px-3"
                            color="black"
                            @click="changeDisplay(true)"
                        >
                            mdi-table
                        </v-icon>
                        <span @click="setSize(5)" class="av-item-selector font-weight-bold">5</span>
                        <span @click="setSize(10)" class="av-item-selector px-3 font-weight-bold">10</span>
                        <span @click="setSize(15)" class="av-item-selector font-weight-bold">15</span>
                    </v-col>
                </v-row>
                <v-card v-if="showTable" class="mx-8 mt-4">
                    <v-data-table
                        :headers="headers"
                        :items="usersFiltered"
                        :page.sync="page"
                        :items-per-page="itemsPerPage"
                        hide-default-footer
                        class="elevation-1"
                        @page-count="pageCount = $event"
                    >
                        <template #item.status="{ item }">
                            <!-- <v-btn 
                                rounded
                                class="py-6 av-status"
                                width="150"
                                :color="statusColor(item.status)"
                                
                            >
                                {{ item.status }}
                            </v-btn> -->
                            <v-chip
                                class="av-status"
                                text-color="white"
                                large
                                :color="statusColor(item.status)"
                            >
                                {{ item.status }}
                            </v-chip>
                        </template>
                        <template #item.actions>
                            <Selector class="mt-4"/>
                        </template>
                    </v-data-table>
                    <div class="text-center py-6">
                        <v-pagination
                            v-model="page"
                            :length="pageCount"
                        ></v-pagination>
                    </div>
                </v-card>
                <v-row v-else>

                <v-card v-for="user in usersFiltered"
                    :key="user.name"
                    height="350"
                    width="320"
                    class="ma-8"
                >
                    <v-card-title class="d-flex justify-center">
                        <v-icon size="120">mdi-shield-account</v-icon>
                    </v-card-title>
                    <v-card-subtitle class="mt-2 ml-2">
                        <div>
                            <span class="font-weight-bold">Nombre:</span> {{ user.name }}
                        </div>
                        <div>
                            <span class="font-weight-bold">Clinica:</span> {{ user.clinic }}
                        </div>
                        <div>
                            <span class="font-weight-bold">Objetivo Tratamiento:</span> {{ user.traitement }}
                        </div>
                        <div>
                            <span class="font-weight-bold">Estado:</span> {{ user.status }}
                        </div>
                    </v-card-subtitle>
                    <v-card-actions>
                        <Selector/> 
                    </v-card-actions>
                </v-card>
                </v-row>
            </v-col>
        </v-row>
    </v-container>
</template>

<script>
import SubHeader from './SubHeader'
import Selector from './Selector'
import users from '../../assets/users.json'
export default {
    components: {
        SubHeader,
        Selector
    },
    data: () => ({
        headers: [
            {
               text : 'Nombres Y Apellidos',
               align: 'start',
               value: 'name'
            },
            { text: 'Clinica', value: 'clinic'},
            { text: 'Objetivo Tratamiento', value: 'traitement'},
            { text: 'Estado', value: 'status'},
            { text: 'Acciones', value: 'actions', sortable: false}
        ], 
        users,
        usersForTable : [],
        searchByName: '',
        showTable: true,
        itemsPerPage : 5,
        page: 1,
        pageCount: 0,
    }),
    computed: {
        usersFiltered() {
            if (!this.searchByName) {
                return this.usersForTable
            }

            const filtered = this.usersForTable.filter(user => user.name.search(this.searchByName) !== -1)

            if (!this.showTable) {
                return filtered.slice(0, this.itemsPerPage)
            }

            return filtered
        },
    },
    methods: {
        changeDisplay(value) {
            this.showTable = value
        },
        setSize(value) {
            this.itemsPerPage = value
        },
        editItem(value) {
            console.log(value)
        },
        statusColor(status) {
            if (status === 'aceptado') return 'blue'
            if (status === 'facturado') return 'green'
            if (status === 'solitado' || status === 'solucitado') return 'yellow'
            if (status === 'enviado') return 'purple'
            if (status === 'planificando') return 'orange'
            else return 'red'
        },
        createCSV() {
            const csvContent = this.usersFiltered.reduce((acc, user) => {
                acc += `Name: ${user.name}, Traitement: ${user.traitement}, Clinic: ${user.clinic}, Status: ${user.status}\n`
                return acc
            }, 'data:text/csv;charset=utf-8,')
            const encodedUri = encodeURI(csvContent);
            window.open(encodedUri);
        }
    },
    created() {
        this.usersForTable = Object.keys(this.users).reduce((acc, key) => {
            const user = this.users[key]
            const { datos_paciente, ficha_dental } = user
            const { nombre, apellidos } = datos_paciente
            const { clinica, objetivo_tratamiento, estado } = ficha_dental
            acc.push({ 
                name: `${nombre} ${apellidos}`,
                clinic: clinica,
                traitement: objetivo_tratamiento,
                status: estado,
                key
            })
            return acc
        }, [])
    }
}
</script>

<style lang="scss" scoped>
.av-body {
    height: 100%;
}
.av-container {
    max-width: 100%;
}
.av-middle-shadow {
    height: 100%;
    box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 25px 0 rgba(0, 0, 0, 0.19);
}
.av-item-selector {
    cursor: pointer;
}
.av-status {
    width: 120px;
    justify-content: center;
}
</style>

<template>
    <v-container class="px-0 av-container">
        <v-row class="av-bar mx-0">
            <span class="py-4 pl-10">
                Listado de Pacientes
            </span>
        </v-row>
    </v-container>
</template>

<script>

export default {
    data: () => ({
        test:1,
    }),
}
</script>

<style lang="scss" scoped>
.av-container {
    max-width: 100%;
}
.av-bar {
    background-color: #E0E0E0;
}
</style>
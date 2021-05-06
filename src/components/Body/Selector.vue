<template>
    <v-select
        :items="values"
        label="Acciones"
        outlined
        v-model="action"
    />
</template>

<script>
export default {
    data: () => ({
        values: [ 'Editar', 'Finalizar', 'Borrar'],
        action: ''
    })
}
</script>

<style lang="scss" scoped>

</style>
<template>
  <v-row class="av-bar">
      <v-spacer></v-spacer>
      <v-col 
        cols="2"
        class="mt-2"
        align-self="center"
      >
            <v-icon
                color="white"
                large
                class="pr-2"
            >
                mdi-account-circle
            </v-icon>
            <span>Dr. pablo Kehyaian</span>
            <v-icon
                color="white"
                class="pl-2"
            >
                mdi-chevron-down
            </v-icon>
      </v-col>
  </v-row>
</template>

<script>
export default {

}
</script>

<style lang="scss" scoped>
.av-bar {
    background-color: #333333;
}
</style>
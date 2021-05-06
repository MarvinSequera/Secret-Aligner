<template>
  <v-app>
    <v-main>
      <Header/>
      <Body/>
    </v-main>
  </v-app>
</template>

<script>
import Header from './components/Header'
import Body from './components/Body/Body'
export default {
  name: 'App',

  components: {
    Header,
    Body,
  },

  data: () => ({
    //
  }),
};
</script>

<template>
  <v-app>
    <Nav />
    <v-content>
      <router-view></router-view>
    </v-content>
    <Footer />
  </v-app>
</template>

<script>
import Footer from '~/components/Footer'
import Nav from '~/components/Nav'

export default {
  components: {
    Footer, Nav
  },
  data(){
    return {
      
    }
  },
}
</script>

<style scoped>
.v-toolbar{
  flex: none !important;
}
</style>

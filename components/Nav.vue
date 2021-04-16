<template>
  <v-toolbar app>
      <v-toolbar-title>
        <router-link to="/" tag="span" style="cursor: pointer">
          {{ appTitle }}
        </router-link>
      </v-toolbar-title>
      <v-spacer></v-spacer>
      <v-toolbar-items class="hidden-xs-only">
        <v-btn
          text
          v-for="item in links"
          :key="item.index"
          :to="item.url">
          {{ item.name }}
        </v-btn>
      </v-toolbar-items>
    </v-toolbar>
</template>

<script>

export default {
    data(){
        return {
            appTitle: 'Awesome App',
            links: [],
            messages: []
        }
    },
    mounted() {
        this.getMenus();
    },
    methods: {
        async getMenus() {
            let res = await this.$axios.get('/header?token=9d04c2c980aab37a16976b463a3df8776e402444963bb92fd4456c1eca354xyz');
            let links = res.data.header.links;
            if(res.data.success){
                this.links = links;
            }else{
                this.messages = res.messages;
            }
        },
    }
}
</script>

<style>

</style>
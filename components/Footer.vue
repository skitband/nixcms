<template>
    <v-footer
      :padless="padless"
    >
    <v-row
      justify="center"
      no-gutters
    >
      <v-btn
        v-for="link in links"
        :key="link.index"
        :to="link.url"
        text
        class="my-3"
      >
        {{ link.name }}
      </v-btn>
      <v-col
        class="text-center white--text my-3"
        cols="12"
      >
        <strong v-html="copyright"></strong>
      </v-col>
    </v-row>

    </v-footer>
</template>

<script>
export default {
    data(){
        return {
            padless: true,
            links: [],
            messages: [],
            copyright: '',
        }
    },
    mounted() {
        this.getFooter();
    },
    methods: {
        async getFooter() {
            let res = await this.$axios.get('/footer?token=9d04c2c980aab37a16976b463a3df8776e402444963bb92fd4456c1eca354xyz');
            let datas = res.data.footer;
            if(res.data.success){
                this.links = datas.links;
                this.copyright = datas.copyright;
            }else{
                this.messages = res.messages;
            }
        },
    }
}
</script>
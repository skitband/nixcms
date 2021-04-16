<template>
  <article>
    <v-container>
        <div class="">
          <section v-for="(section, sectionIdx) in datas" :key="'section-'+ sectionIdx">
            <h2 class="pt-5">{{ section.name }}</h2>
            <div class="row">
              <div class="col" v-for="(content, contentIdx) in section.contents" :key="'section-' + sectionIdx + '-content-' + contentIdx">
                <h3>{{ content.title }}</h3>
                <p v-html="content.body"></p>
                <p v-html="content.address"></p>
                <span v-html="content.contact_number_1"></span>
                <br>
                <span v-html="content.contact_number_2"></span>
                <br>
                <a v-html="content.email"></a>
              </div>
              <!-- <pre>{{ section.section_type }}</pre> -->
              <div class="col" v-if="section.section_type.code == 'ContactForm' ">
                <p>Please fill in your details below</p>
                <v-form v-model="valid" @submit.prevent="submit">
                      <v-text-field
                        v-model="form.name"
                        label="Full Name"
                        required
                      ></v-text-field>
                      <v-text-field
                        v-model="form.position"
                        label="Position"
                        required
                      ></v-text-field>
                      <v-text-field
                        v-model="form.company_name"
                        label="Company"
                        required
                      ></v-text-field>
                      <v-text-field
                        v-model="form.email"
                        :rules="emailRules"
                        label="E-mail"
                        required
                      ></v-text-field>
                      <v-text-field
                        v-model="form.telephone"
                        label="Telephone"
                        required
                      ></v-text-field>
                      <v-text-field
                        v-model="form.fax"
                        label="Fax"
                        required
                      ></v-text-field>
                      <v-textarea
                        v-model="form.message"
                        required
                      >
                      <template v-slot:label>
                        <div>
                          Message
                        </div>
                      </template>
                      </v-textarea>
                      <v-btn block depressed color="primary" type="submit">
                        Submit
                      </v-btn>
                </v-form>
              </div>
            </div>
          </section>
        </div>
      </v-container>
  </article>
</template>

<script>
export default {
    data(){
        return {
            datas: [],
            messages: [],
            sectionTitle: '',
            valid: false,
            form: {
              name: '',
              position: '',
              email: '',
              company_name: '',
              telephone: '',
              fax: '',
              message: ''
            },
            emailRules: [
              v => !!v || 'E-mail is required',
              v => /.+@.+/.test(v) || 'E-mail must be valid',
            ],
        }
    },
    watch: {
        '$route.query'() {
          this.getContents()
        }
    },
    mounted() {
        this.getContents();
    },
    methods: {
        async getContents() {
            let res = await this.$axios.get(`/page/${this.$route.params.slug}?token=9d04c2c980aab37a16976b463a3df8776e402444963bb92fd4456c1eca354xyz`);
            let datas = res.data.page.sections;
            if(res.data.success){
                this.datas = datas;
            }else{
                this.messages = res.messages;
            }
        },
        async submit() {
            let data = this.form;
            let res = await this.$axios.post(`/submit-contact-form?token=9d04c2c980aab37a16976b463a3df8776e402444963bb92fd4456c1eca354xyz`, data);
            let ret = res.data.inquiry;
            if(res.data.success){
              console.log('inquiry', ret)
            }else {
                this.messages = res.messages;
            }
        }
    }
}
</script>

<style>

</style>
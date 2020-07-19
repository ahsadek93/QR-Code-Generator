<template>
  <v-col cols="12">
    <v-card border>
      <v-col cols="12" class="text-center">
        <h2>Welcome to the QR Code Generator tool</h2>
        <p>
          Enter Url Below and click
          <span class="deep-purple--text text-h6">Generate!</span> to get your
          QR code
        </p>
      </v-col>
      <v-col cols="12">
        <v-row justify="center">
          <v-col cols="12" md="6" class="text-center">
            <form>
              <v-text-field
                v-model="url"
                label="URL"
                required
                @input="$v.url.$touch()"
                @blur="$v.url.$touch()"
                :error-messages="urlErrors"
              ></v-text-field>
            </form>
          </v-col>
          <v-col cols="6" md="2" align-self="center">
            <v-row>
              <v-col cols="12" class="text-center">
                <v-btn
                  class="deep-purple accent-4 white--text"
                  @click="submitForm"
                >
                  Generate!
                </v-btn>
              </v-col>
            </v-row>
          </v-col>
        </v-row>
      </v-col>
    </v-card>
  </v-col>
</template>

<script>
import { validationMixin } from 'vuelidate'
import { required, url } from 'vuelidate/lib/validators'
import axios from '@nuxtjs/axios'
import { eventBus } from './../plugins/eventBus'

export default {
  mixins: [validationMixin],

  validations: {
    url: { required, url },
  },

  data() {
    return {
      url: '',
      apiUrlBase: 'https://qrtag.net/api/qr_.png?url=',
      qrCodeImgUrl: '',
    }
  },
  methods: {
    submitForm() {
      this.$v.$touch()
      this.getQr()
      eventBus.$emit('qrCodeGenerated', this.qrCodeImgUrl)
    },

    getQr() {
      this.qrCodeImgUrl = this.apiUrlBase + this.url
    },
  },

  computed: {
    urlErrors() {
      const errors = []
      if (!this.$v.url.$dirty) return errors
      !this.$v.url.url && errors.push('Must be valid URL')
      !this.$v.url.required && errors.push('URL is required')
      return errors
    },
  },
}
</script>

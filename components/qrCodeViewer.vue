<template>
  <v-col cols="12">
    <v-card class="text-center" border>
      <v-row justify="center">
        <v-col align-self="center" cols="5">
          <v-img
            :src="qrCodeImgUrl"
          ></v-img>
        </v-col>
      </v-row>
    </v-card>
  </v-col>
</template>

<script>
import { eventBus } from './../plugins/eventBus'
export default {
  data() {
    return {
      qrCodeImgUrl: '',
    }
  },

  created() {
    eventBus.$on('qrCodeGenerated', url => {
      this.qrCodeImgUrl = url
    })
  },
}
</script>

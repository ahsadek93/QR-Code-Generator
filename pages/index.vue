<template>
  <v-layout>
      <v-container>
        <v-row>
    <headerNav />
    <urlSelector />
    <qrCodeViewer />
     </v-row>
    </v-container>
  </v-layout>
</template>

<script>
import headerNav from './../components/headerNav'
import urlSelector from './../components/urlSelector'
import qrCodeViewer from './../components/qrCodeViewer'

export default {
  components: {
    headerNav,
    urlSelector,
    qrCodeViewer
  },
}
</script>

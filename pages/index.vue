<template>
  <v-row justify="center" align="center">
    <v-col cols="12" sm="8" md="6">
      <div class="text-center">
        <vuetify-logo />
      </div>
      <v-card>
        <v-card-title class="headline">
          Selamat datang di manajemen stock barang
        </v-card-title>
        <v-card-text>
          <p>Manajemen Stock Barang Reseller</p>
          <div class="text-xs-right">
            <em><small>&mdash; Dzikry Kusuma</small></em>
          </div>
          <hr class="my-3" />
          <a
            href="https://nuxtjs.org/"
            target="_blank"
            rel="noopener noreferrer"
          >
            Nuxt Documentation
          </a>
          <br />
          <a
            href="https://github.com/nuxt/nuxt.js"
            target="_blank"
            rel="noopener noreferrer"
          >
            Nuxt GitHub
          </a>
        </v-card-text>
        <v-card-actions>
          <v-spacer />
          <v-btn color="primary" nuxt to="/about"> Continue </v-btn>
        </v-card-actions>
      </v-card>
    </v-col>
  </v-row>
</template>

<script>
import VuetifyLogo from '~/components/VuetifyLogo.vue'

export default {
  components: {
    VuetifyLogo,
  },
}
</script>

<template>
  <v-app dark>
    <v-navigation-drawer
      v-model="drawer"
      :mini-variant="miniVariant"
      :clipped="clipped"
      fixed
      app
    >
      <v-list>
        <template v-for="(item, i) in items">
          <v-list-item
            v-if="$auth.user && item.tipe.includes($auth.user.user_tipe)"
            :key="i"
            :to="item.to"
            router
            exact
          >
            <v-list-item-action>
              <v-icon>{{ item.icon }}</v-icon>
            </v-list-item-action>
            <v-list-item-content>
              <v-list-item-title v-text="item.title" />
            </v-list-item-content>
          </v-list-item>
        </template>
      </v-list>
    </v-navigation-drawer>
    <v-app-bar :clipped-left="clipped" fixed app>
      <v-app-bar-nav-icon @click.stop="drawer = !drawer" />
      <v-btn icon @click.stop="miniVariant = !miniVariant">
        <v-icon>mdi-{{ `chevron-${miniVariant ? 'right' : 'left'}` }}</v-icon>
      </v-btn>
      <v-btn icon @click.stop="clipped = !clipped">
        <v-icon>mdi-application</v-icon>
      </v-btn>
      <v-btn icon @click.stop="fixed = !fixed">
        <v-icon>mdi-minus</v-icon>
      </v-btn>
      <v-toolbar-title v-text="title" />
      <v-spacer />
      <v-btn icon @click.stop="logout">
        {{ $auth.user ? $auth.user.user_nama : 'Belum Login!' }}
      </v-btn>
    </v-app-bar>
    <v-main>
      <v-container>
        <template>
          <nuxt />
        </template>
      </v-container> </v-main
  ></v-app>
</template>

<script>
export default {
  data() {
    return {
      clipped: false,
      drawer: false,
      fixed: false,
      items: [
        {
          tipe: ['admin', 'reseller'],
          icon: 'mdi-home',
          title: 'Dashboard',
          to: '/dashboard-adm',
        },
        {
          tipe: ['admin'],
          icon: 'mdi-domain',
          title: 'Tambah Transaksi',
          to: '/form-transaksi',
        },
        {
          tipe: ['admin'],
          icon: 'mdi-domain',
          title: 'Daftar Tranaksi',
          to: '/list-transaksi',
        },
      ],
      miniVariant: false,
      right: true,
      rightDrawer: false,
      title: 'Manajemen Stock Reseller',
    }
  },

  methods: {
    logout() {
      this.$auth
        .logout()
        .then(() => {
          alert('Logout success')
          this.$router.push('/login')
        })
        .catch(() => {
          alert('Logout failed, please try again.')
        })
    },
  },
}
</script>

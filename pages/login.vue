<template>
  <div>
    <v-container>
      <v-row justify="center">
        <v-col cols="6" md="4">
          <v-form ref="form" class="text-center formku1" lazy-validation>
            <h2 class="title has-text-centered">Login</h2>
            <v-text-field
              v-model="user_hp"
              label="No HP"
              required
              filled
              rounded
            ></v-text-field>
            <v-text-field
              v-model="user_password"
              label="Password"
              type="password"
              required
              filled
              rounded
            ></v-text-field>
            <v-btn class="mr-4" @click="login"> Login </v-btn>
            <v-btn class="mr-4" @click="clear"> Clear </v-btn>
          </v-form>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<script>
export default {
  layout: 'login',
  validations: {
    user_hp: {},
    user_password: {},
  },

  data: () => ({
    user_hp: '',
    user_password: '',
    editedItem: {
      user_id: '',
      user_nama: '',
      user_password: '',
    },
  }),

  methods: {
    async login() {
      try {
        const response = await this.$auth.loginWith('local', {
          data: { user_hp: this.user_hp, user_password: this.user_password },
        })
        if (response) {
          alert('Login sukses')
          this.$router.push({ path: '/dashboard-adm' })
        }
      } catch (err) {
        alert('Login gagal')
      }
    },
    clear() {
      this.user_hp = ''
      this.user_password = ''
    },
    close() {
      this.$nextTick(() => {
        this.editedItem = Object.assign({}, this.defaultItem)
        this.editedIndex = -1
      })
    },
  },
}
</script>

<style>
.formku1 {
  width: 400px;
  margin-top: 35% !important;
}
</style>

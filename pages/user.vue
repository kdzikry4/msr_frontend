<template>
  <v-card>
    <v-card-title>
      User
      <v-spacer></v-spacer>
      <v-text-field
        v-model="search"
        append-icon="mdi-magnify"
        label="Search"
        single-line
        hide-details
      ></v-text-field>
    </v-card-title>
    <v-data-table :headers="headers" :items="users" :search="search">
      <template v-slot:[`item.actions`]="{ item }">
        <v-icon small class="mr-2" @click="editItem(item)"> mdi-pencil </v-icon>
        <v-icon small @click="deleteItem(item)"> mdi-delete </v-icon>
      </template>
    </v-data-table>
  </v-card>
</template>

<script>
export default {
  data() {
    return {
      search: '',
      headers: [
        {
          text: 'Nama',
          align: 'start',
          value: 'user_nama',
        },
        { text: 'Akses User', value: 'user_tipe' },
        { text: 'Nomor HP', value: 'user_hp' },
      ],
      users: [],
      editedItem: { user_nama: '', user_jenis: '', user_hp: '' },
    }
  },

  mounted() {
    this.loadUser()
  },

  methods: {
    async loadUser() {
      const apiusers = await this.$axios.get('/api/users')
      this.users = apiusers.data.values
    },

    editItem(item) {
      this.editedIndex = this.transaksi.indexOf(item)
      this.editedItem = Object.assign({}, item)
      this.dialog = true
    },
  },
}
</script>

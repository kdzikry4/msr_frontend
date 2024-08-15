<template>
  <v-card>
    <v-card-title>
      Barang Tersedia
      <v-spacer></v-spacer>
      <v-text-field
        v-model="search"
        append-icon="mdi-magnify"
        label="Search"
        single-line
        hide-details
      ></v-text-field>
    </v-card-title>
    <v-data-table
      :headers="headers"
      :items="barang"
      :search="search"
    ></v-data-table>
  </v-card>
</template>

<script>
export default {
  data() {
    return {
      search: '',
      headers: [
        {
          text: 'Nama Barang',
          align: 'start',
          sortable: false,
          value: 'barang_nama',
        },
        { text: 'Jenis Barang', value: 'barang_jenis' },
        { text: 'Stock Tersedia', value: 'barang_jumlah' },
      ],
      barang: [],
    }
  },

  mounted() {
    this.loadBarang()
  },

  methods: {
    async loadBarang() {
      const apibarang = await this.$axios.get('/api/barang')
      this.barang = apibarang.data.values
    },
  },
}
</script>

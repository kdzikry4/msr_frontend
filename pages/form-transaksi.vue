<template>
  <v-form ref="form">
    <v-text-field
      v-model="value_transaksi.transaksi_no"
      :rules="nameRules"
      label="Nomor Transaksi"
      required
      readonly
    ></v-text-field>

    <v-select
      v-model="value_transaksi.transaksi_tipe"
      :items="transaksi"
      :rules="[(v) => !!v || 'Item is required']"
      label="Tipe"
      required
    ></v-select>

    <v-text-field
      v-model="value_transaksi.transaksi_catatan"
      label="Catatan"
      required
    ></v-text-field>

    <v-autocomplete
      v-if="value_transaksi.transaksi_tipe == 'Out'"
      v-model="value_transaksi.transaksi_reseller_user"
      :items="reseller"
      item-text="user_nama"
      item-value="user_id"
      :rules="[(v) => !!v || 'Reseller is required']"
      label="Reseller"
      required
    ></v-autocomplete>

    <v-row>
      <v-col
        v-for="(item, index) in value_transaksi.transaksi_item"
        :key="index"
        cols="12"
      >
        <v-autocomplete
          :id="'barang-' + index"
          v-model="value_transaksi.transaksi_item[index].id"
          :items="barang"
          item-text="barang_nama"
          item-value="barang_id"
          :rules="[(v) => !!v || 'Barang is required']"
          label="Barang"
          required
        ></v-autocomplete>
        <v-text-field
          :id="'jumlah-' + index"
          v-model="value_transaksi.transaksi_item[index].jumlah"
          label="Jumlah Barang"
          required
        ></v-text-field>
      </v-col>
    </v-row>
    <v-btn color="success" class="mr-4" @click="save"> Simpan </v-btn>

    <v-btn color="error" class="mr-4" @click="reset"> Reset Form</v-btn>

    <v-btn color="info" class="mr-4" @click="tambahBarang">
      Tambah Barang</v-btn
    >
  </v-form>
</template>

<script>
export default {
  data: () => ({
    transaksi: ['In', 'Out'],
    reseller: [],
    barang: [],
    value_transaksi: {
      transaksi_no: '',
      transaksi_tipe: '',
      transaksi_catatan: '',
      transaksi_reseller_user: '',
      transaksi_item: [],
    },
  }),
  mounted() {
    this.reset()
    this.loadBarang()
    this.loadReseller()
  },
  methods: {
    reset() {
      this.$refs.form.reset()
      this.value_transaksi.transaksi_no = Date.now()
      this.value_transaksi.transaksi_item = [this.barangKosong()]
    },

    async loadBarang() {
      const apibarang = await this.$axios.get('/api/barang')
      this.barang = apibarang.data.values
    },

    async loadReseller() {
      const apiUser = await this.$axios.get('/api/users?reseller=true')
      this.reseller = apiUser.data.values
    },

    async save() {
      const apicreatetransaksi = await this.$axios.post('/api/transaksi', {
        transaksi_no: this.value_transaksi.transaksi_no,
        transaksi_tipe: this.value_transaksi.transaksi_tipe,
        transaksi_catatan: this.value_transaksi.transaksi_catatan,
        transaksi_reseller_user: this.value_transaksi.transaksi_reseller_user,
        transaksi_item: this.value_transaksi.transaksi_item,
      })
      if (apicreatetransaksi.data.status === 200) {
        alert('Transaksi berhasil disimpan')
        this.reset()
      } else {
        alert('Transaksi Gagal')
      }
    },

    tambahBarang() {
      this.value_transaksi.transaksi_item.push(this.barangKosong())
    },

    barangKosong() {
      return {
        id: '',
        jumlah: '',
      }
    },
  },
}
</script>

<style type="css">
.col {
  max-width: 45%;
}
</style>

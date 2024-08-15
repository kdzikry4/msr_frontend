<template>
  <div>
    <v-row>
      <v-col cols="12">
        <h2>Tersedia</h2>
      </v-col>
    </v-row>
    <v-row>
      <v-col cols="12" md="3">
        <template>
          <v-card class="mx-auto" max-width="344">
            <v-card-text>
              <div>Atasan</div>
              <p class="text-h4 text--primary">{{ tersedia.atasan }}</p>
            </v-card-text>
          </v-card>
        </template>
      </v-col>
      <v-col cols="12" md="3">
        <template>
          <v-card class="mx-auto" max-width="344">
            <v-card-text>
              <div>Bawahan</div>
              <p class="text-h4 text--primary">{{ tersedia.bawahan }}</p>
            </v-card-text>
          </v-card>
        </template>
      </v-col>
      <v-col cols="12" md="3">
        <template>
          <v-card class="mx-auto" max-width="344">
            <v-card-text>
              <div>Outer</div>
              <p class="text-h4 text--primary">{{ tersedia.outer }}</p>
            </v-card-text>
          </v-card>
        </template>
      </v-col>
      <v-col cols="12" md="3">
        <template>
          <v-card class="mx-auto" max-width="344">
            <v-card-text>
              <div>Total</div>
              <p class="text-h4 text--primary">{{ tersedia.total }}</p>
            </v-card-text>
          </v-card>
        </template>
      </v-col>
    </v-row>

    <v-row>
      <v-col cols="12">
        <h2>Terjual</h2>
      </v-col>
    </v-row>
    <v-row>
      <v-col cols="12" md="3">
        <template>
          <v-card class="mx-auto" max-width="344">
            <v-card-text>
              <div>Atasan</div>
              <p class="text-h4 text--primary">{{ terjual.atasan }}</p>
            </v-card-text>
          </v-card>
        </template>
      </v-col>
      <v-col cols="12" md="3">
        <template>
          <v-card class="mx-auto" max-width="344">
            <v-card-text>
              <div>Bawahan</div>
              <p class="text-h4 text--primary">{{ terjual.bawahan }}</p>
            </v-card-text>
          </v-card>
        </template>
      </v-col>
      <v-col cols="12" md="3">
        <template>
          <v-card class="mx-auto" max-width="344">
            <v-card-text>
              <div>Outer</div>
              <p class="text-h4 text--primary">{{ terjual.outer }}</p>
            </v-card-text>
          </v-card>
        </template>
      </v-col>
      <v-col cols="12" md="3">
        <template>
          <v-card class="mx-auto" max-width="344">
            <v-card-text>
              <div>Total</div>
              <p class="text-h4 text--primary">{{ terjual.total }}</p>
            </v-card-text>
          </v-card>
        </template>
      </v-col>
    </v-row>

    <v-row>
      <v-col cols="12">
        <h2>Transaksi</h2>
      </v-col>
    </v-row>
    <v-row>
      <v-col cols="12" md="3">
        <template>
          <v-card class="mx-auto" max-width="344">
            <v-card-text>
              <div>Transaksi Out</div>
              <p class="text-h4 text--primary">{{ transaksi.out }}</p>
            </v-card-text>
          </v-card>
        </template>
      </v-col>
    </v-row>
  </div>
</template>

<script>
export default {
  data() {
    return {
      tersedia: {
        atasan: 0,
        bawahan: 0,
        outer: 0,
        total: 0,
      },
      terjual: {
        atasan: 0,
        bawahan: 0,
        outer: 0,
        total: 0,
      },
      transaksi: {
        out: 0,
      },
      liveId: null,
    }
  },

  mounted() {
    this.loadAll()
    this.liveId = setInterval(this.loadAll, 3000)
  },

  beforeDestroy() {
    if (this.liveId) {
      clearInterval(this.liveId)
    }
  },

  methods: {
    loadAll() {
      this.loadTersedia()
      this.loadTerjual()
      this.loadTransaksi()
    },
    async loadTersedia() {
      const apiTersedia = await this.$axios.get('/api/dashboard-tersedia')
      const barang = apiTersedia.data.values
      for (let i = 0; i < barang.length; i++) {
        if (barang[i].barang_jenis === 'atasan') {
          this.tersedia.atasan = barang[i].tersedia
        }
        if (barang[i].barang_jenis === 'bawahan') {
          this.tersedia.bawahan = barang[i].tersedia
        }
        if (barang[i].barang_jenis === 'outer') {
          this.tersedia.outer = barang[i].tersedia
        }
      }
      this.tersedia.total =
        this.tersedia.atasan + this.tersedia.bawahan + this.tersedia.outer
    },
    async loadTerjual() {
      const apiTerjual = await this.$axios.get('/api/dashboard-terjual')
      const barang = apiTerjual.data.values
      for (let i = 0; i < barang.length; i++) {
        if (barang[i].barang_jenis === 'atasan') {
          this.terjual.atasan = barang[i].terjual
        }
        if (barang[i].barang_jenis === 'bawahan') {
          this.terjual.bawahan = barang[i].terjual
        }
        if (barang[i].barang_jenis === 'outer') {
          this.terjual.outer = barang[i].terjual
        }
      }
      this.terjual.total =
        this.terjual.atasan + this.terjual.bawahan + this.terjual.outer
    },
    async loadTransaksi() {
      const apiTransaksi = await this.$axios.get('/api/dashboard-transaksi')
      const transaksi = apiTransaksi.data.values
      this.transaksi.out = transaksi[0].transaksi_out
    },
  },
}
</script>

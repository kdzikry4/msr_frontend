<template>
  <v-row justify="center">
    <v-col class="text-center">
      <v-form ref="form" lazy-validation>
        <v-text-field label="Nama" required></v-text-field>
        <v-text-field label="Nomor HP" required></v-text-field>
        <v-select label="Pilih Ruang" :items="items" required></v-select>
        <v-btn color="success" class="mr-4">Submit</v-btn>
        <v-btn color="error" class="mr-4" @click="reset">Reset Form</v-btn>
      </v-form>
    </v-col>
  </v-row>
</template>

<script>
export default {
  data: () => ({
    items: ['Admin', 'Reseller'],
    date: new Date().toISOString().substr(0, 10),
    menu: false,
  }),

  methods: {
    reset() {
      this.$refs.form.reset()
    },
  },
}
</script>

<style type="css">
.col {
  max-width: 45%;
}
</style>

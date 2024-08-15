<template>
  <v-form ref="form" v-model="valid" lazy-validation>
    <v-text-field
      v-model="user_nama"
      :counter="10"
      :rules="nameRules"
      label="Name"
      required
    ></v-text-field>

    <v-text-field
      v-model="user_hp"
      :rules="emailRules"
      label="Nomor HP"
      required
    ></v-text-field>

    <v-select
      v-model="user_jenis"
      :items="items"
      :rules="[(v) => !!v || 'Item is required']"
      label="Item"
      required
    ></v-select>

    <v-text-field
      v-model="user_password"
      :rules="emailRules"
      label="Password"
      required
    ></v-text-field>

    <v-btn :disabled="!valid" color="success" class="mr-4" @click="validate">
      Validate
    </v-btn>

    <v-btn color="error" class="mr-4"> Reset Form</v-btn>

    <v-btn color="warning" @click="resetValidation"> Reset Validation </v-btn>
  </v-form>
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

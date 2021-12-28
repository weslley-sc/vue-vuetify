<template>
     <v-card width="500" class="mx-auto mt-5">
        <v-card-title><h1 class="display-1">Login</h1></v-card-title>
        <v-card-text>
          <v-form>
            <v-text-field
              label="Username"
              prepend-icon="mdi-account-circle"
            ></v-text-field>
            <v-text-field
              label="Password"
              prepend-icon="mdi-lock"
              :append-icon="exibir ? 'mdi-eye' : 'mdi-eye-off'"
              :type="exibir ? 'text' : 'password'"
              @click:append="showhide"
            ></v-text-field>
          </v-form>
        </v-card-text>
        <v-card-actions>
          <v-btn color="success" to="/register">Register</v-btn>
          <v-spacer></v-spacer>
          <v-btn color="info">Login</v-btn>
        </v-card-actions>
      </v-card>
</template>
<script>
export default {
      data: () => ({
    exibir: false,
    links: ["Home", "Login", "About"],
  }),
   methods: {
    showhide() {
      this.exibir = !this.exibir;
    },
  },
}
</script>
<style scoped>

</style>
<template>
  <v-form ref="form" v-model="valid" lazy-validation>
    <v-container>
      <v-text-field
        v-model="name"
        :counter="10"
        :rules="nameRules"
        label="Name"
        required
      ></v-text-field>

      <v-text-field
        v-model="email"
        :rules="emailRules"
        label="E-mail"
        required
      ></v-text-field>
      <v-row>
        <v-col cols="3">
          <v-text-field
            label="CEP"
            @blur="getCEP"
            v-model="cep"
            type="number"
          ></v-text-field>
        </v-col>
        <v-col cols="">
          <v-text-field label="Cidade" v-model="cidade"></v-text-field>
        </v-col>
        <v-col>
          <v-text-field label="Estado" v-model="estado"></v-text-field>
        </v-col>
      </v-row>

      <v-select
        v-model="select"
        :items="items"
        :rules="[(v) => !!v || 'Item is required']"
        label="Item"
        required
      ></v-select>

      <v-checkbox
        v-model="checkbox"
        :rules="[(v) => !!v || 'You must agree to continue!']"
        label="Do you agree?"
        required
      ></v-checkbox>

      <v-btn :disabled="!valid" color="success" class="mr-4" @click="validate">
        Validate
      </v-btn>

      <v-btn color="error" class="mr-4" @click="reset"> Reset Form </v-btn>

      <v-btn color="warning" @click="resetValidation"> Reset Validation </v-btn>
    </v-container>
  </v-form>
</template>
<script>
export default {
  data: () => ({
    cep: "",
    cepRules : [
        (v) => (v.length == 8 || "CEP invalido")
    ],
    cidade: "",
    estado: "",
    valid: true,
    name: "",
    nameRules: [
      (v) => !!v || "Name is required",
      (v) => (v && v.length <= 10) || "Name must be less than 10 characters",
    ],
    email: "",
    emailRules: [
      (v) => !!v || "E-mail is required",
      (v) => /.+@.+\..+/.test(v) || "E-mail must be valid",
    ],
    select: null,
    items: ["Item 1", "Item 2", "Item 3", "Item 4"],
    checkbox: false,
  }),

  methods: {
    validate() {
      this.$refs.form.validate();
    },
    reset() {
      this.$refs.form.reset();
    },
    resetValidation() {
      this.$refs.form.resetValidation();
    },

    async getCEP() {
        if(this.cep.length ===8 ) {
                  try {
        const response = await fetch(
          `https://viacep.com.br/ws/${this.cep}/json/`
        );
        const json = await response.json();
        console.log(json);
        this.cidade = json.localidade;
        this.estado = json.uf;
      } catch (error) {
          console.log("CEP Inválido", error);
      }
        } else {
            console.log("CEP Inválido")
        }

    },
  },
};
</script>
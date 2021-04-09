<template>
  <v-container>
    <v-row>
      <v-col>
        <h1>Signup</h1>
        <v-form ref="signUpForm" v-model="formValidity">
          <v-text-field
            label="Email"
            type="email"
            v-model="email"
            :rules="emailRules"
          ></v-text-field>
          <v-autocomplete
            label="Which browser do you use?"
            :items="browsers"
          ></v-autocomplete>
          <v-file-input label="Attach profile picture"></v-file-input>
          <v-text-field
            label="Birthday"
            v-model="birthday"
            readonly
          ></v-text-field>
          <v-date-picker v-model="birthday"></v-date-picker>
          <v-checkbox
            label="Agree to terms &amp; conditions"
            v-model="agreeToTerms"
            :rules="agreeToTermsRules"
          ></v-checkbox>
          <v-btn
            type="submit"
            color="primary"
            class="mr-4"
            :disabled="!formValidity"
            >Submit</v-btn
          >
          <v-btn color="success" class="mr-4" @click="validateForm"
            >Validate Form</v-btn
          >
          <v-btn color="warning" @click="resetValidation" class="mr-4"
            >Reset Validation</v-btn
          >
          <v-btn color="error" @click="resetForm" class="mr-4"
            >Reset Form</v-btn
          >
        </v-form>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      browsers: ["Google Chrome", "Firefox", "Edge", "Safari", "Brave"],
      birthday: "",
      agreeToTerms: false,
      agreeToTermsRules: [
        (value) =>
          !!value ||
          "You must agree to the terms & conditions to signup for an account",
      ],
      email: "",
      emailRules: [
        (value) => !!value || "Email is required.",
        (value) => value.indexOf("@") !== 0 || "Email should have a username.",
        (value) => value.includes("@") || "Email should include an @ symbol.",
        (value) =>
          value.indexOf(".") - value.indexOf("@") > 1 ||
          "Email should include a valid domain.",
        (value) =>
          value.indexOf(".") <= value.length - 3 ||
          "Email shoul contain a valid domain extension.",
      ],
      formValidity: false,
    };
  },
  methods: {
    resetValidation() {
      this.$refs.signUpForm.resetValidation();
    },
    resetForm() {
      this.$refs.signUpForm.reset();
    },
    validateForm() {
      this.$refs.signUpForm.validate();
    },
  },
};
</script>

<style lang="scss" scoped></style>

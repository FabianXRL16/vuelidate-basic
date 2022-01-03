<template>
  <div class="formContainer">
    <h2 class="mb-4 text-center">Formulario de Prueba</h2>
    <form @submit.prevent="submitForm" class="">
      <div>
        <div class="form-group mb-2">
          <label>Name</label>
          <input type="text" v-model="name" class="form-control" />
          <span v-if="!$v.name.required && $v.name.$dirty" class="text-danger"
            >Name is required!</span
          >
          <span v-if="!$v.name.alpha && $v.name.$dirty" class="text-danger"
            >Name is required!</span
          >
        </div>
        <div class="form-group mb-2">
          <label>Email</label>
          <input type="email" v-model="email" class="form-control" />
          <span
            v-if="(!$v.email.required || !$v.email.email) && $v.email.$dirty"
            class="text-danger"
            >Valid Email is required!</span
          >
        </div>
        <div class="form-group mb-2">
          <label>Password</label>
          <input type="password" v-model="password" class="form-control" />
          <span
            v-if="!$v.password.required && $v.password.$dirty"
            class="text-danger"
            >Password is required!</span
          >
          <span
            v-if="!$v.password.minLength || !$v.password.maxLength"
            class="text-danger"
            >Passsword must be between
            {{ $v.password.$params.minLength.min }} and
            {{ $v.password.$params.maxLength.max }} characters!</span
          >
        </div>
        <div class="form-group mb-2">
          <label>Gender</label>
          <select v-model="gender" class="form-control">
            <option value="male">Male</option>
            <option value="female">Female</option>
            <option value="other">Other</option>
          </select>
          <span
            v-if="!$v.gender.required && $v.gender.$dirty"
            class="text-danger"
            >Gender is required!</span
          >
        </div>
        <div class="form-check mb-2 d-flex justify-content-center gap-2">
          <input
            type="checkbox"
            v-model="acceptTerms"
            class="form-check-input"
          />
          <label class="form-check-label"> Accept Terms</label>
        </div>
        <span
          v-if="!$v.acceptTerms.required && $v.acceptTerms.$dirty"
          class="text-danger"
          >Accept Terms is required!</span
        >
        <br />
      </div>
      <input type="submit" class="btn btn-primary" />
    </form>
  </div>
</template>

<script>
import {
  required,
  minLength,
  maxLength,
  alpha,
  email,
} from "vuelidate/lib/validators";
export default {
  name: "VuelidateForm",
  props: {},
  data() {
    return {
      name: "",
      email: "",
      password: "",
      gender: "",
      acceptTerms: "",
    };
  },
  validations: {
    name: {
      required,
      alpha,
    },
    email: {
      required,
      email,
    },
    password: {
      required,
      minLength: minLength(6),
      maxLength: maxLength(12),
    },
    gender: {
      required,
    },
    acceptTerms: {
      required,
    },
  },
  methods: {
    submitForm() {
      this.$v.$touch();

      if (!this.$v.$invalid) {
        console.log(
          `Name: ${this.name}, Email: ${this.email}, Password: ${this.password}, Gender: ${this.gender}, AcceptTerms: ${this.acceptTerms}`
        );
      }
    },
  },
};
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Roboto&display=swap");
.formContainer {
  font-family: "Roboto", sans-serif;
  background-color: rgba(188, 213, 223, 0.445);
  width: 400px;
  height: 85vh;
  border-radius: 10px;
  padding: 30px;
  box-sizing: border-box;
  color: rgb(129, 166, 180);
}
form {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  width: 100%;
  height: calc(100% - 36.41px - 24px);
  box-sizing: border-box;
}
</style>
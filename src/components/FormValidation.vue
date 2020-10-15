<template>
  <div class="card">
    <h3 class="card-header text-center">Register</h3>
    <div class="card-body">
      <form @submit.prevent="submitForm">
        <div class="form-row">
          <div class="form-group col-md-6">
            <label>First Name</label>
            <input type="text" class="form-control"
            v-model.trim="$v.firstname.$model" :class="{
            'is-invalid':$v.firstname.$error, 'is-valid':!$v.firstname.$invalid }">
              <div class="valid-feedback"> Your firstname is valid! </div>
              <div class="invalid-feedback">
                <span v-if="!$v.firstname.required"> first name is required. </span>
                <span v-if="!$v.firstname.minLength"> first name must have at least {{
                  $v.firstname.$params.minLength.min }} letters</span>
                <span v-if="!$v.firstname.maxLength"> first name must have at most {{
                  $v.firstname.$params.maxLength.max }} letters </span>
              </div>
          </div>
          <div class="form-group col-md-6">
            <label>Last Name</label>
            <input type="text" class="form-control" v-model.trim="$v.lastname.$model"
            :class="{ 'is-invalid':$v.lastname.$error,
            'is-valid':!$v.lastname.$invalid }">
              <div class="valid-feedback"> Your lastname is valid! </div>
              <div class="invalid-feedback">
                <span v-if="!$v.lastname.required"> last name is required. </span>
                <span v-if="!$v.lastname.minLength">l ast name must have at least {{
                  $v.lastname.$params.minLength.min }} letters </span>
                <span v-if="!$v.lastname.maxLength"> last name must have at most {{
                  $v.lastname.$params.maxLength.max }} letters </span>
              </div>
          </div>
        </div>
        <div class="form-group">
          <label>username</label>
          <input type="text" class="form-control" v-model.trim="$v.username.$model"
          :class="{ 'is-invalid':$v.username.$error, 'is-valid':!$v.username.$invalid }">
          <div class="valid-feedback">Your username is valid!</div>
          <div class="invalid-feedback">
            <span v-if="!$v.username.required"> Username is required </span>
            <span v-if="!$v.username.isUnique"> This username is already registered </span>
          </div>
        </div>
        <div class="form-group">
          <label>Email</label>
          <input type="text" class="form-control" v-model.trim="$v.email.$model"
          :class="{ 'is-invalid':$v.email.$error, 'is-valid':!$v.email.$invalid }">
          <div class="valid-feedback">Your email is valid!</div>
          <div class="invalid-feedback">
            <span v-if="!$v.email.required"> Email is required </span>
            <span v-if="!$v.email.isUnique"> This email is already registered </span>
          </div>
        </div>
        <div class="form-group">
          <label>Password</label>
          <input type="password" id="password" class="form-control"
          v-model.trim="$v.password.$model"
          :class="{ 'is-invalid':$v.password.$error, 'is-valid':!$v.password.$invalid }">
          <div class="valid-feedback">Your password is valid!</div>
          <div class="invalid-feedback">
            <span v-if="!$v.password.required"> password is required </span>
            <span v-if="!$v.password.minLength"> {{ $v.password.$parmas.minLength.min }}
            characters min </span>
          </div>
        </div>
        <div class="form-group form-check">
          <input type="checkbox" id="showpassword" class="form-check-input"
          @click="toggleShowPassword" v-model="showpassword">
          <label class="form-check-label" for="showpassword"> Show password </label>
        </div>
        <div class="form-group">
          <label>Repeat Password</label>
          <input type="password" class="form-control" v-model.trim="$v.repeatpassword.$model"
          :class="{ 'is-invalid':$v.repeatpassword.$error, 'is-valid': (password != '') ?
          !$v.repeatpassword.$invalid : '' }">
          <div class="valid-feedback">Your password is identical!</div>
          <div class="invalid-feedback">
            <span v-if="!$v.repeatpassword.sameAsPassword"> Password must be identical.</span>
          </div>
        </div>
        <button type="submit" class="btn btn-success">Submit {{ submitstatus }}</button>
      </form>
    </div>
  </div>
</template>

<script>
import {
  required, minLength, maxLength, email, sameAs,
} from 'vuelidate/lib/validators';

export default {
  name: 'FormValidation',
  data() {
    return {
      firstname: '',
      lastname: '',
      username: '',
      email: '',
      password: '',
      repeatpassword: '',
      showpassword: false,
      submitstatus: null,
    };
  },
  validations: {
    firstname: {
      required,
      minLength: minLength(3),
      maxLength: maxLength(10),
    },
    lastname: {
      required,
      minLength: minLength(3),
      maxLength: maxLength(15),
    },
    username: {
      required,
      isUnique(value) {
        if (value === '') return true;
        return new Promise((resolve) => {
          setTimeout(() => {
            resolve(typeof value === 'string' && value.length % 2 !== 0);
          }, 350 + Math.random() * 300);
        });
      },
    },
    email: {
      required,
      email,
      isUnique(value) {
        if (value === '') return true;

        return new Promise((resolve) => {
          setTimeout(() => {
            resolve(typeof value === 'string' && value.length % 2 !== 0);
          }, 350 + Math.random() * 300);
        });
      },
    },
    password: {
      required,
      minLength: minLength(8),
    },
    repeatpassword: {
      sameAsPassword: sameAs('password'),
    },
  },
  methods: {
    toggleShowPassword() {
      const show = document.getElementById('password');
      if (this.showpassword === false) {
        this.showpassword = true;
        show.type = 'text';
      } else {
        this.showpassword = false;
        show.type = 'password';
      }
    },
    submitForm() {
      this.$v.$touch();
      if (this.$v.$invalid) {
        this.submitstatus = 'FAIL';
      } else {
        this.submitstatus = 'SUCCES';
      }
    },
  },
};
</script>

<style scoped>
.card-body {
  text-align:start;
}
</style>

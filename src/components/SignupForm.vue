<template>
  <div class="signupform">
    <div id="logo" >
      <img alt="Vue logo" src="../assets/logo.png">
    </div>
    <form @submit.prevent="handleSubmit">
      
      <md-field :class="{'md-input-invalid': errors.has('name')}">
        <label>Name</label>
        <md-input v-model="name" v-validate name="name" data-vv-rules="required"></md-input>
      </md-field>
      <span class="md-error">{{errors.first('name')}}</span>

      <md-field :class="{'md-input-invalid': errors.has('email')}">
        <label>Epost</label>
        <md-input v-model="email" v-validate name="email" data-vv-rules="required|email"></md-input>
      </md-field>
      <span class="md-error">{{errors.first('email')}}</span>
      
      <md-field :class="{'md-input-invalid': errors.has('company')}">
        <label>Företag</label>
        <md-input v-model="company" v-validate name="company" data-vv-rules="required"></md-input>
      </md-field>
      <span class="md-error">{{errors.first('company')}}</span>
      
      <md-field>
        <label>Specialkost</label>
        <md-input v-model="specialDiet"></md-input>
      </md-field>
      
      <transition name="fade">
        <div class="submit-message success" v-if="ok">Anmälan lyckades!</div>
      </transition>

      <transition name="fade">
        <div class="submit-message error" v-if="submitError">{{submitError}}</div>
      </transition>
      
      <div class="center">
        <md-button class="md-raised md-primary" type="submit">Anmäl</md-button>
      </div>
    </form>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
import VeeValidate from 'vee-validate';
import VueMaterial from 'vue-material'
import 'vue-material/dist/vue-material.min.css'

import db from '../db'

export default Vue.extend({
  name: 'SignupForm',
  data: () => ({
    validate: false,
    ok: false,
    submitError: '',
    name: '',
    email: '',
    company: '',
    specialDiet: '',
  }),
  methods: {
    handleSubmit() {
      if (this.errors.any()) {
        this.submitError = "Formuläret innehåller fel. Vänligen rätta till dessa och försök igen"
        return
      }
      const {
        name,
        email,
        company,
        specialDiet,
      } = this
      db.collection('applications').add({
        name,
        email,
        company,
        specialDiet,
      })
      .then(() => this.ok = true)
      .catch(err => this.submitError = err)
    }
  }
})

Vue.use(VueMaterial)
Vue.use(VeeValidate)
</script>

<style scoped>
.signupform {
  justify-self: center;
  grid-column-start: 2;
  min-width: 450px;
  align-self: center;
  padding: 20px;
}

#logo {
  margin: auto;
  width: 150px;
  height: 150px;
}

#logo img {
  max-width: 100%;
  max-height: 100%;
}

.center {
  width: 90px;
  margin: auto;
}

.submit-message {
  width: 100%;
  padding: 15px;
  text-align: center;
}

.success {
  background-color: #47c93747;
  border: 1px solid green;
  color: green;
}

.error {
  background-color: #FF000047;
  border: 1px solid #9a0000;
  color: #9a0000;
}

.md-error {
  margin-top: -20px;
  display: block;
  color: red;
}

.fade-enter-active, .fade-leave-active {
  transition: opacity .5s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
  opacity: 0;
}

.md-primary {
  color: white;
  background-color: #c2c937;
}
input {
  border-bottom: 1px solid #d4d4d4 !important;
}
input:focus{
  border-bottom: 1px solid green !important;
}
</style>


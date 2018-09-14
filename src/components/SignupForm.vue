<template>
  <div class="signupform">
    <div id="logo" >
      <img alt="Vue logo" src="../assets/logo.png">
    </div>
    <form @submit.prevent="handleSubmit">
      <md-field>
        <label>Name</label>
        <md-input v-model="name"></md-input>
      </md-field>
      <md-field>
        <label>Epost</label>
        <md-input v-model="email"></md-input>
      </md-field>
      <md-field>
        <label>Företag</label>
        <md-input v-model="company"></md-input>
      </md-field>
      <md-field>
        <label>Specialkost</label>
        <md-input v-model="specialDiet"></md-input>
      </md-field>
      <transition name="fade">
        <div class="success" v-if="ok">Anmälan lyckades!</div>
      </transition>
      <div class="center">
        <md-button class="md-raised md-primary" type="submit">Anmäl</md-button>
      </div>
    </form>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
import VueMaterial from 'vue-material'
import 'vue-material/dist/vue-material.min.css'

import db from '../db'

export default Vue.extend({
  name: 'SignupForm',
  data: () => ({
    validate: false,
    ok: false,
    error: '',
    name: '',
    email: '',
    company: '',
    specialDiet: '',
  }),
  methods: {
    handleSubmit() {
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
      .catch(err => this.error = err)
    }
  }
})

Vue.use(VueMaterial)
</script>

<style lang="postcss" scoped>
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

.success {
  width: 100%;
  padding: 15px;
  text-align: center;
  background-color: #47c93747;
  border: 1px solid green;
  color: green;
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


<template>
  <div id="app">
    <div id="logo" >
      <img alt="Vue logo" src="./assets/logo.png">
    </div>
    <SignupForm />
  </div>
</template>

<script>
import SignupForm from './components/SignupForm.vue'

export default {
  name: 'app',
  components: {
    SignupForm
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

#logo {
  width: 100px;
  height: 100px;
}

#logo img {
  max-width: 100%;
  max-height: 100%;
}
</style>

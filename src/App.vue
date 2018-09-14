<template>
  <div id="app">
    <div class="main">
      <OverviewText />
      <SignupForm />
    </div>
  </div>
</template>

<script>
import SignupForm from './components/SignupForm.vue'
import OverviewText from './components/OverviewText.vue'

export default {
  name: 'app',
  components: {
    SignupForm,
    OverviewText
  }
}
</script>

<style>
html, body, #app {
  height: 100%;
  width: 100%;
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  display: flex;

  background: url('assets/bg-large.jpg') no-repeat center center fixed; 
  -webkit-background-size: cover;
  -moz-background-size: cover;
  -o-background-size: cover;
  background-size: cover;
}

.main {
  display: inline-grid;
  grid-template-columns: 50% 50%;
  background-color: white;
  width: 100%;
  margin: auto;
  max-width: 1240px;
}
</style>

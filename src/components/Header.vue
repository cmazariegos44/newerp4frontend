<template>
  <div class="header">
    <b-navbar>
      <template slot="brand">
        <b-navbar-item tag="router-link" :to="{ path: '/' }">

          <img
            src="https://raw.githubusercontent.com/buefy/buefy/dev/static/img/buefy-logo.png"
            alt="Lightweight UI components for Vue.js based on Bulma"
          />

        </b-navbar-item>
      </template>
       <template slot="start">
      <b-navbar-item href="#">
          <router-link to="/">Home</router-link>
        </b-navbar-item>
        <b-navbar-item href="#">
          <router-link to="/Page2">About</router-link>
        </b-navbar-item>
        <b-navbar-dropdown label="Info">
          <b-navbar-item href="#">
            About 
          </b-navbar-item>
          <b-navbar-item href="#">
            Contact
          </b-navbar-item>
        </b-navbar-dropdown>
      </template>

      <template slot="end">
        <b-navbar-item tag="div">
          <div class="buttons">
            <a class="button is-primary">
              <strong>Sign up 123</strong>
            </a>
             </div>
           <!-- <a class="button is-light">
              <router-link to="/login">Login in NOW</router-link>
            </a> -->
            <div class="buttons">
              <router-link :to="{ name: 'Login', query: { URL: this.URL }}" v-bind:URL="URL" v-if="!loggedIn"><button class="button is-link">Log in 123</button></router-link>
              <button v-if="loggedIn" class="button is-link" @click="logout">Logout 123</button>
          </div>
        </b-navbar-item>
      </template>
    </b-navbar>
  </div>
</template>

<script>
export default {
    name: 'Header',
    props: ['URL', 'loggedIn'],
    methods: {
        logout: function(){
            this.$emit('logout')
        }
    }
};
</script>

<style>
.header {
    width: 90%;
    margin: 10px auto
}

</style>

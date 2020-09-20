<template>
 <div class="login">
    <b-field label="Username" type="is-success" message="This username is available">
      <b-input v-model="username"></b-input>
    </b-field>

    <b-field label="Password">
      <b-input type="password" v-model="password" password-reveal> </b-input>
    </b-field>
    <br />
    <button class="button is-primary is-light" @click="handleLogin">Log In NOW</button>
  </div> 
</template>

<script>
export default {
  name: "Login",
  data: function() {
    return {
      username: "",
      password: "",
    };
  },
  methods: {
    handleLogin: function() {
      fetch(`https://newp4backend.herokuapp.com/auth/users/login/`, {
        method: "post",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify({
          username: this.username,
          password: this.password,
        }),
      })
        .then((response) => response.json())
        .then((data) => {
          console.log(data);
          this.$emit("loggedIn", data);
        });
    },
  },
};
</script>



<style>
.login {
  width: 70%;
  margin: 10px auto;
}
</style>

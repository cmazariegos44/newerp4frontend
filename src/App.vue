<template>
 <div id="app">
    <!--<div id="nav"> -->
    <Header v-bind:URL="URL" v-bind:loggedIn="loggedIn" @logout="logout" />
    <router-view @loggedIn="login($event)" />  
     <!--</div>-->
    <router-view/>
    <Footer/>
  <div class="main">
    <ul>
      <li v-for="task of task" v-bind:key="task.id">{{ task.message }}</li>
    </ul>
  </div>
 </div>
</template>


<script>
import Header from './components/Header'
import Footer from './components/Footer'

export default {
  name: "App",
  components: {
    Header,
    Footer,
  },

  data: function() {
    return {
      loggedIn: false,
      tokens: {},
      URL: "https://newp4backend.herokuapp.com/auth/users/login/",
      task: [],
      // message: "",
      // editmessage: "",
      // editid: null
    };
} ,
methods: {
    login: function(event) {
      console.log("event heard");
      this.loggedIn = true;
      this.tokens = event;
      this.$router.push("/"
      //   {
      //   path: "Main",
      //   query: { tokens: this.tokens, URL: this.URL },
      // }
      );
    },
    logout: function() {
      this.loggedIn = false;
      this.tokens = {};
      this.$router.push('/')
    },
    //==============================================================
    //NEW TASK METHOD 
     newTask: function() {
      const { tokens, URL } = this.$route.query;

      fetch(`${URL}/task/`, {
        method: "post",
        headers: {
          authorization: `JWT ${tokens}`,
          "Content-Type": "application/json",
        },
        body: JSON.stringify({ message: this.message }),
      }).then(() => {
        this.getTask();
      });
    },


  },//END OF METHOD 



};//END OF EXPORT DEFAULT 
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>

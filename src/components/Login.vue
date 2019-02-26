<template>
  <div>
    <b-form class="login" @submit.prevent="login">
      <h1>Sign in</h1>
      <b-form-group label="Username:" label-for="username">
        <b-form-input required v-model="username"/>
      </b-form-group>

    <b-alert show> {{text}}</b-alert>
     

      <b-form-group label="Password:" label-for="password">
        <b-form-input
          id="password"
          v-model="password"
        />
      </b-form-group>
      <hr>

        <b-button type="submit" variant="primary">Login</b-button>

    </b-form>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  data() {
    return {
      username: "",
      password: "",
      text: 'asdfsdf'
    };
  },
  computed: {
    authStatus() {
      return this.$store.getters.authStatus;
    }
  },
  methods: {
    login() {
        var v = this;
      let {username, password} = this;

       axios({
            url: 'https://employeeauth_dev.msionline.com:9090/api/login',
            data: {
              username,
              password
            },
            method: 'POST'
        })
        .then(res => {
          console.log(res);
          v.text = 'chamged';
        })
    }
  }
};
</script>

<style scoped>
</style>

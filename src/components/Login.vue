<template>
  <div>
    <b-form class="login" @submit.prevent="login">
      <h1>Sign in</h1>
      <b-form-group label="Username:" label-for="username">
        <b-form-input required v-model="username"/>
      </b-form-group>

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
import jwt_decode from 'jwt-decode';

export default {
  data() {
    return {
      username: "",
      password: "",
      token: '',
      decoded: ''
    };
  },
  methods: {
    login() {
      let {username, password} = this;

      axios.post('https://employeeauth_dev.msionline.com:9090/api/login', {
        username, password
      })
      .then(res => {
        console.log(jwt_decode(res.data.token));
        this.$router.push('/')
      })
      .catch(err => console.log(err))
    }
  }
};
</script>

<style scoped>
</style>

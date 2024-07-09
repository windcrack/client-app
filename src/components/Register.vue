<template>
  <div>
    <h2>Register</h2>
    <form @submit.prevent="register">
      <input v-model="username" placeholder="Username" required />
      <input v-model="password" type="password" placeholder="Password" required />
      <button type="submit">Register</button>
    </form>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      username: '',
      password: ''
    };
  },
  methods: {
    register() {
      axios.post('http://localhost:3300/auth/register', {
        username: this.username,
        password: this.password
      })
      .then(response => {
        alert('User registered');
      })
      .catch(error => {
        console.error(error);
      });
    }
  }
};
</script>
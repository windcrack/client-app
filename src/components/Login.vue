<template>
  <div>
    <h2>Login</h2>
    <form @submit.prevent="login">
      <input v-model="username" placeholder="Username" required />
      <input v-model="password" type="password" placeholder="Password" required />
      <button type="submit">Login</button>
    </form>
    <div v-if="user">
      <p>Welcome, {{ user.username }}!</p>
      <p>Your role: {{ user.role }}</p>
      <button @click="logout">Logout</button>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      username: '',
      password: '',
      user: null
    };
  },
  created() {
    this.checkAuth();
  },
  methods: {
    login() {
      axios.post('http://localhost:3300/auth/login', {
        username: this.username,
        password: this.password
      })
      .then(response => {
        this.user = response.data;
        localStorage.setItem('user', JSON.stringify(this.user));
      })
      .catch(error => {
        console.error(error);
      });
    },
    logout() {
      axios.get('http://localhost:3300/auth/logout')
      .then(() => {
        this.user = null;
        localStorage.removeItem('user');
      })
      .catch(error => {
        console.error(error);
      });
    },
    checkAuth() {
      const storedUser = localStorage.getItem('user');
      if (storedUser) {
        this.user = JSON.parse(storedUser);
      } else {
        axios.get('http://localhost:3300/auth/current_user')
        .then(response => {
          this.user = response.data;
          localStorage.setItem('user', JSON.stringify(this.user));
        })
        .catch(() => {
          this.user = null;
        });
      }
    }
  }
};
</script>
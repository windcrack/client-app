<template>
  <div id="app">
    <Register />
    <Login />
    <Logout />
  </div>
</template>

<script>
import Register from './components/Register.vue';
import Login from './components/Login.vue';
import Logout from './components/Logout.vue';

export default {
  components: {
    Register,
    Login,
    Logout
  }
};
</script>
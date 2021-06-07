<template>
<div>
  <v-app-bar color="deep-purple accent-4"
      dense
      dark>
      <v-toolbar-title>Tab Tracker</v-toolbar-title></v-app-bar>

<v-container>
  <v-row>
    <v-col xl="6"
        offset-xl="3">
      <v-card
        elevation="12"
      >
      <div class="white elevation-2">
        <v-toolbar dense dark>
          <v-toolbar-title> Register </v-toolbar-title>
        </v-toolbar>
      </div>
      <br>
      <div>
        <input
          type="email"
          name="email"
          v-model="email"
          placeholder="Email" />
        <br>
        <input
          type="password"
          name="password"
          v-model="password"
          placeholder="Password" />
        <br>
        <div v-html="error" class="error"/>
        <br>
        <v-btn class="cyan" @click="register"> Register </v-btn>
    </div>
</v-card>
    </v-col>
  </v-row>
</v-container>
</div>
</template>

<script>
import AuthenticationService from '@/services/AuthenticationService'
export default {
  name: 'register',
  data () {
    return {
      email: '',
      password: '',
      error: ''
    }
  },
  methods: {
    async register () {
      try {
        const response = await AuthenticationService.register({
          email: this.email,
          password: this.password
        })
        console.log(response.data)
        this.error = ''
      } catch (err) {
        this.error = err.response.data.error
      }
    }
  }
}
</script>

<style scoped>
  .error{
    color: red;
  }

  input{
    border-bottom: 1px solid black;
    margin: 20px 20px 20px 20px;
    width: 75%;
  }
</style>

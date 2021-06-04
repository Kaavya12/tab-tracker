<template>
  <v-layout column>
    <v-flex xs6 offset-xs3>
      <div class="white elevation-2">
        <v-toolbar dense dark>
          <v-toolbar-title> Register </v-toolbar-title>
        </v-toolbar>
      </div>
      <br>
      <div class="pl-4 pr-4 pt-2 pb-2">
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
    </v-flex>
  </v-layout>

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
</style>

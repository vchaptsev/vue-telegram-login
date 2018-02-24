<template>
  
  <!-- Callback mode -->
  <vue-telegram-login 
    mode="callback"
    telegram-login="YourTelegramBot"
    @callback="yourCallbackFunction" />
  
  <!-- Redirect mode -->
  <vue-telegram-login 
    mode="redirect"
    telegram-login="YourTelegramBot"
    redirect-url="https://your-website.io" />

</template>

<script>
import {vueTelegramLogin} from 'vue-telegram-login'

export default {
  name: 'your-component',
  components: {vueTelegramLogin},
  methods: {
    yourCallbackFunction (user) {
      // gets user as an input
      // id, first_name, last_name, username,
      // photo_url, auth_date and hash
      console.log(user)
    }
  }
}
</script>
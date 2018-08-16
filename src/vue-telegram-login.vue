<template>
  <div ref="telegram"></div>
</template>

<script>
export default {
  name: 'vue-telegram-login',
  props: {
    mode: {
      type: String,
      required: true,
      validator (value) { return ['callback', 'redirect'].includes(value) }
    },
    telegramLogin: {
      type: String,
      required: true,
      validator (value) { return value.endsWith('bot') || value.endsWith('Bot') }
    },
    redirectUrl: {
      type: String,
      default: ''
    },
    requestAccess: {
      type: String,
      default: 'read',
      validator (value) { return ['read', 'write'].includes(value) }
    },
    size: {
      type: String,
      default: 'large',
      validator (value) { return ['small', 'medium', 'large'].includes(value) }
    },
    userpic: {
      type: Boolean,
      default: true
    },
    radius: {
      type: String
    }
  },
  methods: {
    onTelegramAuth (user) {
      this.$emit('callback', user)
    }
  },
  mounted () {
    // create script with given params
    const script = document.createElement('script')
    script.async = true
    script.src = 'https://telegram.org/js/telegram-widget.js?3'

    script.setAttribute('data-size', this.size)
    script.setAttribute('data-userpic', this.userpic)
    script.setAttribute('data-telegram-login', this.telegramLogin)
    script.setAttribute('data-request-access', this.requestAccess)
    if (this.radius) { script.setAttribute('data-radius', this.radius) }

    if (this.mode === 'callback') {
      window.onTelegramAuth = this.onTelegramAuth
      script.setAttribute('data-onauth', 'window.onTelegramAuth(user)')
    } else {
      script.setAttribute('data-auth-url', this.redirectUrl)
    }

    this.$refs.telegram.appendChild(script)
  }
}
</script>

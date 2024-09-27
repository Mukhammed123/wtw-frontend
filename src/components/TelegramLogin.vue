<template>
  <div>
    <h1>Авторизация через Telegram</h1>
    <div id="telegram-login"></div>
  </div>
</template>

<script>
import { onMounted } from 'vue'
import { useUserStore } from '@/stores/user'
import { useRouter } from 'vue-router'
import axios from 'axios'

export default {
  setup() {
    const router = useRouter()
    const userStore = useUserStore()

    window.onTelegramAuth = function (user) {
      const userData = {
        id: user.id,
        first_name: user.first_name,
        last_name: user.last_name,
        username: user.username
      }

      axios
        .post('http://5.59.232.33:85/test/users', userData)
        .then((response) => {
          userStore.setUser(response.data)
          router.push('/dashboard')
        })
        .catch((error) => {
          console.error('Error sending data to backend:', error)
        })
    }

    onMounted(() => {
      const script = document.createElement('script')
      script.setAttribute('src', 'https://telegram.org/js/telegram-widget.js?22')
      script.setAttribute('data-telegram-login', 'WebTgWalletBot')
      script.setAttribute('data-size', 'large')
      script.setAttribute('data-onauth', 'onTelegramAuth(user)')
      script.setAttribute('data-request-access', 'write')
      script.async = true

      document.getElementById('telegram-login-container').appendChild(script)
    })

    return {}
  }
}
</script>

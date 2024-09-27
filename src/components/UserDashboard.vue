<template>
  <div>
    <h2>Привет, {{ userData.first_name }}</h2>
    <p>Ваш текущий баланс: {{ balance }} единиц</p>

    <h3>Перевод средств</h3>
    <form @submit.prevent="transferFunds">
      <label
        >Telegram ID получателя:
        <input v-model="recipientId" type="text" required />
      </label>
      <br />
      <label
        >Сумма:
        <input v-model="amount" type="number" required />
      </label>
      <br />
      <button type="submit">Отправить средства</button>
    </form>
    <p>{{ message }}</p>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  props: {
    userData: Object
  },
  data() {
    return {
      balance: 1000,
      recipientId: '',
      amount: 0,
      message: ''
    }
  },
  methods: {
    async transferFunds() {
      try {
        const response = await axios.post('URL', {
          userId: this.userData.id,
          recipientId: this.recipientId,
          amount: this.amount
        })
        this.balance -= this.amount
        this.message = response.data.message
      } catch (error) {
        this.message = 'Ошибка перевода средств: ' + error.response.data.detail
      }
    }
  }
}
</script>

<script setup>
import { reactive } from 'vue'
import { AsyncpayCheckout } from '@asyncpay/checkout'

const state = reactive({
  firstName: '',
  lastName: '',
  email: '',
  amount: 10
})

const handleCheckout = () => {
  AsyncpayCheckout({
    publicKey: import.meta.env.VITE_APP_PUBLIC_KEY,
    customer: {
      firstName: state.firstName,
      lastName: state.lastName,
      email: state.email
    },
    amount: state.amount,
    onSuccess: () => {
      // Run a function to process the payment
      alert('Payment successful')
    },
    onClose: () => {
      // Run a function whenever the user closes the popup regardless of the payment status
    }
  })
}
</script>

<template>
  <section>
    <h1>A Simple Asyncpay Checkout</h1>
    <hr />
    <form @submit.prevent="handleCheckout">
      <div>
        <label for="firstName">First Name</label>
        <input name="firstName" type="text" v-model="state.firstName" />
      </div>
      <div>
        <label for="lastName">Last Name</label>
        <input name="lastName" type="text" v-model="state.lastName" />
      </div>
      <div>
        <label for="email">Email</label>
        <input name="email" type="email" v-model="state.email" />
      </div>
      <div>
        <label for="amount">Amount</label>
        <input type="number" v-model="state.amount" />
      </div>
      <div>
        <button>Pay NGN {{ state.amount }}</button>
      </div>
    </form>
  </section>
</template>

<style scoped>
label {
  display: block;
}
section {
  padding: 30px;
}

form {
  display: flex;
  flex-direction: column;
  gap: 8px;
}
</style>

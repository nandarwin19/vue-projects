<template>
  <h3>Add new transaction</h3>
  <form id="form" @submit.prevent="onSubmit">
    <div class="form-control">
      <label for="text">Text</label>
      <input type="text" id="text" placeholder="Enter text..." v-model="text" />
    </div>
    <div class="form-control">
      <label for="amount"
        >Amount <br />
        (negative - expense, positive - income)
      </label>
      <input type="text" id="amount" placeholder="Enter amount..." v-model="amount" />
    </div>
    <button class="btn">Add transaction</button>
  </form>
</template>

<script setup>
import { ref } from 'vue'
import { useToast } from 'vue-toast-notification'

const text = ref('')
const amount = ref('')

const toast = useToast()

const emit = defineEmits(['addTransaction'])

const onSubmit = () => {
  // console.log('hi', text.value, amount.value)
  if (!text.value || !amount.value) {
    toast.error('Please fill both field!')
    return
  }

  const transactionData = {
    text: text.value,
    amount: parseFloat(amount.value)
  }

  emit('addTransaction', transactionData)

  text.value = ''
  amount.value = ''
}
</script>

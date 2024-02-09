<template>
    <h3>Add new transaction</h3>
    <form id="form" @submit.prevent="addTransaction">
        <div class="form-control">
            <input v-model="transactionName" type="text" id="text" placeholder="Enter Transaction name..." />
        </div>
        <div class="form-control">
            <label for="amount">(Make amount Negative for expense, e.g -2000)</label>
            <input v-model="transactionAmount" type="text" id="amount" placeholder="Enter amount..." />
        </div>
        <button class="btn">Add transaction</button>
    </form>
</template>

<script setup>
import { ref, defineProps } from 'vue';

const emit = defineEmits(['transactionAdded'])

const transactionName = ref("")
const transactionAmount = ref("")
const props = defineProps({
    transactions: { type: Array, required: true }
})

function addTransaction() {
    const transaction = {
        name: transactionName.value,
        amount: Number(transactionAmount.value)
    }
    console.log("transaction added", transaction)
    emit('transactionAdded', transaction)
    transactionName.value = ''
    transactionAmount.value = ''
}

</script>
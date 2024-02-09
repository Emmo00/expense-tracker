<template>
    <h3>Add new transaction</h3>
    <form id="form" @submit.prevent="addTransaction">
        <div class="form-control">
            <label for="text">Text</label>
            <input v-model="transactionName" type="text" id="text" placeholder="Enter text..." />
        </div>
        <div class="form-control">
            <label for="amount">Amount <br />
                (negative - expense, positive - income)</label>
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
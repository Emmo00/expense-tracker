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

const transactionName = ref("")
const transactionAmount = ref("")
const props = defineProps({
    transactions: { type: Array, required: true }
})

function addTransaction() {
    const randomNumber = Math.floor(Math.random() * 100)
    props.transactions.push({ id: randomNumber, text: transactionName.value, amount: Number(transactionAmount.value) })
    transactionName.value = ''
    transactionAmount.value = ''
}

</script>
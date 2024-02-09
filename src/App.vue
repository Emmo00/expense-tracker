<template>
    <HeaderVue />
    <div class="container">
        <div>
            <Balance>
                {{ total }}
            </Balance>
            <IncomeExpense :income="totalIncome.toFixed(2)" :expense="totalExpense.toFixed(2)" />
            <TransactionList :transactions="transactions" @transactionDeleted="deleteTransaction"
                @clearTransactions="clearTransactions" />
        </div>
        <AddTransaction :transactions="transactions" @transactionAdded="addTransaction" />
    </div>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue'
import HeaderVue from './components/Header.vue';
import Balance from './components/Balance.vue';
import IncomeExpense from './components/IncomeExpense.vue';
import TransactionList from './components/TransactionList.vue';
import AddTransaction from './components/AddTransaction.vue';

const transactions = ref([
])

onMounted(() => {
    const savedTransactions = JSON.parse(localStorage.getItem('transactions'))
    if (savedTransactions) {
        transactions.value = savedTransactions
    }
})

const total = computed(() => transactions.value.reduce((acc, transaction) => transaction.amount + acc, 0))
const totalIncome = computed(() => transactions.value.filter(transaction => transaction.amount > 0).reduce((acc, transaction) => transaction.amount + acc, 0))
const totalExpense = computed(() => transactions.value.filter(transaction => transaction.amount < 0).reduce((acc, transaction) => transaction.amount + acc, 0))

function addTransaction({ name, amount }) {
    transactions.value.push({
        id: Math.floor(Math.random() * 100),
        name,
        amount
    })
    console.log(transactions.value)
    updateLocalStorage()
}

function deleteTransaction(id) {
    transactions.value = transactions.value.filter(transaction => transaction.id !== id)
    updateLocalStorage()
}

function clearTransactions() {
    transactions.value = []
    updateLocalStorage()
}

function updateLocalStorage() {
    localStorage.setItem('transactions', JSON.stringify(transactions.value))
}
</script>

<style scoped>
.container>div {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
}
</style>
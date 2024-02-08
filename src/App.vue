<template>
    <HeaderVue />
    <div class="container">
        <Balance>
            {{ total }}
        </Balance>
        <IncomeExpense :income="totalIncome.toFixed(2)" :expense="totalExpense.toFixed(2)" />
        <TransactionList :transactions="transactions" />
        <AddTransaction :transactions="transactions"/>
    </div>
</template>

<script setup>
import { ref, computed } from 'vue'
import HeaderVue from './components/Header.vue';
import Balance from './components/Balance.vue';
import IncomeExpense from './components/IncomeExpense.vue';
import TransactionList from './components/TransactionList.vue';
import AddTransaction from './components/AddTransaction.vue';

const transactions = ref([
    { id: 1, text: "Flowers", amount: -18.99 },
    { id: 2, text: "Salary", amount: 800 },
    { id: 3, text: "Camera", amount: -28.99 }
])

const total = computed(() => transactions.value.reduce((acc, transaction) => transaction.amount + acc, 0))

const totalIncome = computed(() => transactions.value.filter(transaction => transaction.amount > 0).reduce((acc, transaction) => transaction.amount + acc, 0))
const totalExpense = computed(() => transactions.value.filter(transaction => transaction.amount < 0).reduce((acc, transaction) => transaction.amount + acc, 0))
</script>
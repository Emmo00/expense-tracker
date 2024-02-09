<template>
    <h3>History</h3>
    <ul id="list" class="list">
        <li :class="transaction.amount < 0 ? 'minus' : 'plus'" v-for="transaction in transactions" :key="transaction.id">
            {{ transaction.name }} <span>{{ transaction.amount }}</span><button class="delete-btn"
                @click="deleteTransaction(transaction.id)">x</button>
        </li>
    </ul>
</template>

<script setup>
import { defineProps } from 'vue';

const emit = defineEmits(['transactionDeleted'])
const props = defineProps({ transactions: { type: Array, required: true } })

function deleteTransaction(id) {
    emit('transactionDeleted', id)
}

</script>

<style scoped>
li {
    margin-left: 10px;
}
</style>

<template>
<!-- смена названий переменных
     msgs -> expenses
     msg -> expense
     addMsg -> addExpense
     deleteMsg -> deleteExpense -->
  <div class="card">
    <input type="text" placeholder="+ add name">
    <div v-for="expense in card.expenses" :key="expense.id" class="prosto">
      <input
        type="number"
        v-model="expense.value"
        placeholder="+ Add number"
      />
      <button @click="deleteExpense(expense)">X</button>
    </div>
    <button @click="addExpense">+ Add more</button>
    <div class="sum">Card Total: {{ cardTotal }}</div>
  </div>
</template>

<script>
export default {
  props: {
    card: {
      type: Object,
      required: true,
    },
  },
  computed: {
    cardTotal() {
      return this.card.expenses.reduce((acc, expense) => {
        const value = parseInt(expense.value || 0, 10);
        return acc + value;
      }, 0);
    },
  },
  methods: {
    deleteExpense(expense) {
      this.$emit('delete', this.card, expense);
    },
    addExpense() {
      this.$emit('add', this.card);
    },
  },
};
</script>

<style scoped>
.card {
  display: flex;
  flex-direction: column;
}
</style>
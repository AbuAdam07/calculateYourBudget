<template>
  <h2>Income: {{ TotalIncomeSum }}</h2>
  <div class="income">
    <div v-for="card in incomeCards" :key="card.id">
      <IncomeCard
        :card="card"
        @delete="deleteIncomeMsg"
        @add="addNewIncomeMsg"
      />
      <button @click="deleteIncomeCard(card)">X</button>
    </div>
    <button @click="addIncomeCard">
      + Add card <br /><br />
    </button>
  </div>
  <h2>Outcome : {{ TotalOutcomeSum }}</h2>
  <div class="outcome">
    <div v-for="card in outcomeCards" :key="card.id">
      <OutcomeCard
        :card="card"
        @delete="deleteOutcomeExpense"
        @add="addNewOutcomeExpense"
      />
      <button @click="deleteOutcomeCard(card)">X</button>
    </div>
    <button @click="addOutcomeCard">
      + Add card <br /><br />
    </button>
  </div>
  <h1>TOTAL RESULT : {{ TotalIncomeSum - TotalOutcomeSum }}</h1>
</template>

<script>
import IncomeCard from "./components/IncomeCard.vue";
import OutcomeCard from "./components/OutcomeCard.vue";

export default {
  data() {
    return {
      incomeCards: [{ id: 1, msgs: [] }],
      outcomeCards: [{ id: 1, expenses: [] }],
      incomesTotal: 0,
      cardsTotal: 0,
    };
  },
  methods: {
    addIncomeCard() {
      const newCard = { id: Date.now(), msgs: [] };
      this.incomeCards.push(newCard);
    },
    deleteIncomeCard(cardToDelete) {
      this.incomeCards = this.incomeCards.filter(
        (card) => card.id !== cardToDelete.id
      );
    },
    addOutcomeCard() {
      const newCard = { id: Date.now(), expenses: [] };
      this.outcomeCards.push(newCard);
    },
    deleteOutcomeCard(cardToDelete) {
      this.outcomeCards = this.outcomeCards.filter(
        (card) => card.id !== cardToDelete.id
      );
    },
    deleteIncomeMsg(card, msg) {
      card.msgs = card.msgs.filter((t) => t.id !== msg.id);
    },
    addNewIncomeMsg(card) {
      const newMsg = { id: Date.now(), value: "" };
      card.msgs.push(newMsg);
    },
    deleteOutcomeExpense(card, expense) {
      card.expenses = card.expenses.filter((t) => t.id !== expense.id);
    },
    addNewOutcomeExpense(card) {
      const newExpense = { id: Date.now(), value: "" };
      card.expenses.push(newExpense);
    },
  },
  computed: {
    TotalIncomeSum() {
      return this.incomeCards.reduce((acc, card) => {
        return (
          acc +
          card.msgs.reduce((accMsg, curMsg) => {
            const sum = parseInt(curMsg.value, 10) || 0;
            return accMsg + sum;
          }, 0)
        );
      }, 0);
    },
    TotalOutcomeSum() {
      return this.outcomeCards.reduce((acc, card) => {
        return (
          acc +
          card.expenses.reduce((accExpense, curExpense) => {
            const sum = parseInt(curExpense.value, 10) || 0;
            return accExpense + sum;
          }, 0)
        );
      }, 0);
    },
  },
  components: {
    IncomeCard,
    OutcomeCard,
  },
};
</script>

<style scoped>
.income {
  display: flex;
}
.outcome {
  display: flex;
}
</style>

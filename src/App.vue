<template>
  <div class="income">
    <div v-for="card in cards" :key="card.id">
      <Card :card="card" @delete="deleteMsg" @add="addNewMsg" />
      <button @click="deleteCard(card)">X</button>
    </div>
    <button @click="addCard">+ Add card <br><br>TOTAL = {{ TotalIncomeSum }}</button>
  </div>
</template>

<script>
import Card from "./components/Card.vue";

export default {
  data() {
    return {
      cards: [{ id: 1, msgs: [] }],
      incomesTotal: 0,
      cardsTotal: 0,
    };
  },
  methods: {
    addCard() {
      const newCard = { id: Date.now(), msgs: [] };
      this.cards.push(newCard);
    },
    deleteCard(cardToDelete) {
      this.cards = this.cards.filter((card) => card.id !== cardToDelete.id);
    },
    deleteMsg(card, msg) {
      card.msgs = card.msgs.filter((t) => t.id !== msg.id);
    },
    addNewMsg(card) {
      const newMsg = { id: Date.now(), value: "" };
      card.msgs.push(newMsg);
    },
  },
  computed: {
    TotalIncomeSum() {
      return this.cards.reduce((acc, card) => {
        return (
          acc + card.msgs.reduce(
            (accMsg, curMsg) => {
            const sum = parseInt(curMsg.value, 10) || 0;
            return accMsg + sum;
            }, 0
          )
        );
      }, 0);
    },
  },
  components: {
    Card,
  },
};
</script>
<style scoped>
.income {
  display: flex;
}
</style>

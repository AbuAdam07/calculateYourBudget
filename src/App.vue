<template>
  <div class="main">
    <div class="container">
      <h2>Income: {{ TotalIncomeSum }}</h2>
      <div class="income">
        <div v-for="card in incomeCards" :key="card.id" class="bat">
          <IncomeCard
            :card="card"
            @delete="deleteIncomeMsg"
            @add="addNewIncomeMsg"
          />
          <button
            class="btn btn-secondary btn_x"
            @click="deleteIncomeCard(card)"
          >
            X
          </button>
        </div>
        <button class="btn btn-secondary btn_ad" @click="addIncomeCard">
          + Add card <br /><br />
        </button>
      </div>
      <h2>Outcome : {{ TotalOutcomeSum }}</h2>
      <div class="outcome">
        <div v-for="card in outcomeCards" :key="card.id" class="bat">
          <OutcomeCard
            :card="card"
            @delete="deleteOutcomeExpense"
            @add="addNewOutcomeExpense"
          />
          <button
            class="btn btn-secondary btn_x"
            @click="deleteOutcomeCard(card)"
          >
            X
          </button>
        </div>
        <button class="btn btn-secondary btn_ad" @click="addOutcomeCard">
          + Add card <br /><br />
        </button>
      </div>
      <h1>TOTAL RESULT : {{ TotalIncomeSum - TotalOutcomeSum }}</h1>
    </div>
  </div>
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
@import url("https://fonts.googleapis.com/css2?family=Anta&family=Arimo:ital@0;1&family=Barlow:wght@600&family=Inter:slnt,wght@-10..0,100..900&family=Josefin+Sans:ital,wght@0,100..700;1,100..700&family=Lato:ital,wght@0,100;0,300;0,400;0,700;0,900;1,100;1,300;1,400;1,700;1,900&family=Open+Sans:wght@400;600;700;800&family=Poppins:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;0,800;0,900;1,100;1,200;1,300;1,400;1,500;1,600;1,700;1,800;1,900&display=swap");
* {
  box-sizing: border-box;
  margin: 0 auto;
  padding: 2%;
  font-size: 100%;
  list-style: none;
}
body {
  font-family: "Josefin Sans", sans-serif;
  font-optical-sizing: auto;
  font-style: normal;
}
h1 {
  font-family: "Josefin Sans", sans-serif;
  font-size: 2em;
  color: white;
}
h2 {
  font-size: 1.5em;
  color: white;
}
.btn {
  color: azure;
  text-align: center;
}

@keyframes slide {
  0% {
    background-position: 0% 0%;
  }
  50% {
    background-position: 100% 0%;
  }
  100% {
    background-position: 100% 0%;
  }
}
.main {
  background-image: url(../public/office.jpg);
  background-repeat: cover;
  animation: slide 90s linear infinite;
  width: 100%;
  height: 100%;
}
.income {
  display: flex;
  font-family: "Josefin Sans", sans-serif;
  flex-wrap: wrap;
}
.outcome {
  display: flex;
  font-family: "Josefin Sans", sans-serif;
  flex-wrap: wrap;
}
.bat {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}
.btn_x {
  background-color: red;
}
.btn_ad{
  background-color: rgb(55, 164, 0);
  align-self: center;
  text-align: center;
  padding: 5px;
  margin: 0 auto;
  border-color: yellow;
}
</style>

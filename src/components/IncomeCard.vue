<template>
  <div class="card">
    <input type="text" placeholder="+ add name">
    <div v-for="msg in card.msgs" :key="msg.id" class="prosto">
      <input
        type="number"
        v-model="msg.value"
        placeholder="+ Add number"
      />
      <button class="btn btn-secondary btn-del" @click="deleteMsg(msg)">X</button>
    </div>
    <button class="btn btn-secondary btn_add" @click="addMsg">+ Add more</button>
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
      return this.card.msgs.reduce((acc, msg) => {
        const value = parseInt(msg.value || 0, 10);
        return acc + value;},0); 
    },
  },
  methods: {
    deleteMsg(msg) {
      this.$emit('delete', this.card, msg);
    },
    addMsg() {
      this.$emit('add', this.card);
    },
  },
};
</script>

<style scoped>
.card {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  text-align: center;
  background-color: #81bbee;
}
input{
  border-radius: 10px;
  margin: 5px;
}
.prosto{
  display: flex;
  flex-direction: row;
}
.btn-del{
  background-color: red;
  height: 2em;
  margin: 5px;
}
.btn_add{
  background-color: rgb(120, 200, 0);
  margin: 5px;
}
.sum{
  padding: 5px;
  color: rgb(253, 253, 0);
}
</style>
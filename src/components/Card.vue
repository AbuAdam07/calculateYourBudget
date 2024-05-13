<template>
  <div class="card">
    <input type="text" placeholder="+ add name">
    <div v-for="msg in card.msgs" :key="msg.id" class="prosto">
      <input
        type="number"
        v-model="msg.value"
        placeholder="+ Add number"
      />
      <button @click="deleteMsg(msg)">X</button>
    </div>
    <button @click="addMsg">+ Add more</button>
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
}
</style>
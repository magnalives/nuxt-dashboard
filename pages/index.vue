<template>
  <div>
    <Card
      :cardData="cards"
      v-on:removecard="removeCard"
      v-on:addcards="addcards"
    />
  </div>
</template>

<script>
import Card from "~/components/cards";
export default {
  components: {
    Card
  },
  data() {
    return {
      cards: [],
      minCard: 0,
      maxCard: 10
    };
  },
  mounted() {
    this.$axios.get("https://jsonplaceholder.typicode.com/todos/").then(res => {
      this.cards = res.data.slice(this.minCard, this.maxCard);
    });
  },
  methods: {
    removeCard() {
      this.cards = this.cards.splice(1, this.cards.length);
    },
    addcards() {
      this.minCard += 7;
      this.maxCard += 7;
      this.$axios
        .get("https://jsonplaceholder.typicode.com/todos/")
        .then(res => {
          let newcards = res.data.slice(this.minCard, this.maxCard);
          console.log(newcards);

          this.cards = newcards;
        });
    }
  }
};
</script>

<style scoped></style>

<template>
  <div>
    <div v-for="card in cards" :key="card.id">
      {{ card.id }}
    </div>
    <button @click="removeCard">Remove by one</button>
  </div>
</template>

<script>
export default {
  props: ["cardData"],
  data() {
    return {};
  },
  computed: {
    cards: function() {
      return this.cardData;
    }
  },
  watch: {
    cards: function() {
      if (this.cards.length < 4) {
        this.$emit("addcards");
      }
    }
  },
  methods: {
    removeCard() {
      this.$emit("removecard");
    }
  }
};
</script>

<style></style>

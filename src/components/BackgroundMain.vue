<template>
  <div>
    <NavBar @card-added="handleCardAdded" />
    <div class="container">
      <h1>Notes</h1>
      <div class="main-content d-flex flex-wrap align-content-start">
        <NoteCard
          v-for="card in cards"
          :key="card.id"
          :id="String(card.id)"
          :description="card.description"
          :color="card.color"
          @delete-card="handleCardDeleted(card.id)"
        />
      </div>
    </div>
  </div>
</template>

<script>
import NavBar from "./NavBar.vue";
import NoteCard from "./NoteCard.vue";

export default {
  name: "BackgroundMain",

  data() {
    return {
      cards: [],
    };
  },

  components: {
    NavBar,
    NoteCard,
  },

  methods: {
    handleCardAdded(newCard) {
      this.cards = [...this.cards, newCard];
    },

    handleCardDeleted(deletedCardId) {
      this.cards = this.cards.filter((card) => card.id !== deletedCardId);
    },

  },
};
</script>

<style scoped>
.container {
  margin-top: 50px;
  height: 94vh;
  display: grid;
  grid-template-columns: repeat(8, 1fr);
  grid-template-rows: repeat(12, 1fr);
}

.container h1 {
  grid-column: 1/2;
  grid-row: 1/2;
}

.container .main-content {
  grid-column: 1/9;
  grid-row: 2/13;
}

.main-content {
  flex-wrap: wrap;
}
</style>

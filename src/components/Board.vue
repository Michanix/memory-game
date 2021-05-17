<template>
  <div>
    <div class="container">
      <div
      class="item"
      v-for="card in reapeatCards"
      :key="card + Math.random() * (10 - 1)"
      v-on:click="onFlip">
        <Card
        :id="card.id"
        :back="card.back"
        :show="card.show"
        />
      </div>
  </div>
  <div v-if="finished">
      <h3>Yey! You have finished the game! It took you {{counter}} steps.</h3>
      <md-button
      class="md-raised md-primary"
      v-on:click="reset">
      Start again!
      </md-button>
  </div>
  </div>
</template>
<script>
import { v4 as uuidv4 } from 'uuid';
import Card from './Card.vue';

const allCards = [
  {
    id: uuidv4(),
    back: 'safari.png',
    show: true,
  },
  {
    id: uuidv4(),
    back: 'dropbox.png',
    show: true,
  },
  {
    id: uuidv4(),
    back: 'facebook.png',
    show: true,
  },
  {
    id: uuidv4(),
    back: 'twitter.png',
    show: true,
  },
  {
    id: uuidv4(),
    back: 'mozilla.png',
    show: true,
  },
  {
    id: uuidv4(),
    back: 'linkdin.png',
    show: true,
  },
];

export default {
  data() {
    return {
      cards: allCards.slice(0, this.size).sort(() => Math.random() - 0.5),
      compare: [],
      counter: 0,
      finished: false,
    };
  },
  components: {
    Card,
  },
  props: {
    size: Number,
  },
  watch: {
    cards() {
      if (this.cards.length === 0) {
        this.finished = true;
      }
    },
  },
  computed: {
    reapeatCards() {
      return Array(2).fill(this.cards).flat(1);
    },
  },
  methods: {
    onFlip(e) {
      const currentCard = e.target.id;
      if (this.compare.length < 2) {
        this.compare.push(currentCard);
      }
      if (this.compare.length === 2) {
        if (this.compare[0] === this.compare[1]) {
          setTimeout(() => {
            this.cards = this.cards
              .filter((card) => card.id !== currentCard);
          }, 1000);
        } else {
          setTimeout(() => {
          }, 500);
        }
        this.compare = [];
        this.flipCounter = 0;
        this.counter += 1;
      }
    },
    reset() {
      window.location.reload();
    },
  },
};
</script>
<style scoped>
.container {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  justify-items: center;
  padding: 10px;
}
.item {
  display: flex;
  align-self: center;
  justify-self: center;
  margin: 0;
}
</style>

<template>
  <div id="app">
    <Toolbar />
    <div class="select" v-if="!selected">
      <select v-model="size" @change="onSelect()">
        <option disabled value="">Please select one</option>
        <option>2</option>
        <option>4</option>
        <option>6</option>
      </select>
    </div>
    <div v-else>
      <Board :size="toInt()"/>
    </div>
  </div>
</template>

<script>
import Toolbar from './components/Toolbar.vue';
import Board from './components/Board.vue';

export default {
  name: 'App',
  data() {
    return {
      size: '',
      selected: false,
    };
  },
  methods: {
    toInt() {
      return parseInt(this.size, 10);
    },
    onSelect() {
      this.selected = !this.selected;
    },
  },
  components: {
    Toolbar,
    Board,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #183858;
}
.select {
  padding: 30px;
}
</style>

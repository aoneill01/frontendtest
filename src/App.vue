<script setup>
import { ref } from "vue";
import Board from "./components/Board.vue";
import Sidebar from "./components/Sidebar.vue";

const history = ref([]);

const handleClick = (square) => {
  history.value.push(square);
};
</script>

<template>
  <h1>Chessboard</h1>
  <main>
    <div>
      <Board class="board" @square-click="handleClick" />
    </div>
    <Sidebar :history="history" />
  </main>
</template>

<style scoped>
h1 {
  display: none;
}

main {
  margin: 16px 16px 0 16px;
  display: flex;
  min-height: calc(100vh - 32px);
  gap: 16px;
}

main > *:first-child {
  flex-grow: 1;
}

.board {
  max-width: calc(100vh - 32px);
  margin: 0 auto;
}
</style>

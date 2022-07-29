<script setup>
import Board from "./components/Board.vue";
import Sidebar from "./components/Sidebar.vue";
</script>

<template>
  <main>
    <div>
      <Board class="board" />
    </div>
    <Sidebar />
  </main>
</template>

<style scoped>
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

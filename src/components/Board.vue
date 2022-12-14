<script setup>
import { computed } from "vue";
import Arrow from "./Arrow.vue";

const emit = defineEmits(["square-click"]);
const props = defineProps(["history"]);

const squares = [];

for (let rankIndex = 0; rankIndex < 8; rankIndex++) {
  for (let fileIndex = 0; fileIndex < 8; fileIndex++) {
    squares.push({
      rank: rankIndex + 1,
      file: String.fromCharCode("a".charCodeAt(0) + fileIndex),
      color: (rankIndex + fileIndex) % 2 === 0 ? "dark" : "light",
    });
  }
}

const lastSelected = computed(() => props.history.at(-1));
const nextToLastSelected = computed(() => props.history.at(-2));

const onClick = (square) => {
  emit("square-click", { file: square.file, rank: square.rank });
};

const isSelected = ({ rank, file }) =>
  rank === lastSelected.value?.rank && file === lastSelected.value?.file;
</script>

<template>
  <div class="board">
    <div
      v-for="square in squares"
      :key="square.file + square.rank"
      :class="[
        'square',
        square.color,
        {
          selected: isSelected(square),
        },
      ]"
      :data-file="square.file"
      :data-rank="square.rank"
      @click="() => onClick(square)"
    ></div>
    <Arrow class="arrow" :from="nextToLastSelected" :to="lastSelected" />
  </div>
</template>

<style scoped>
.board {
  aspect-ratio: 1/1;
  display: grid;
  grid-template-columns: repeat(8, 1fr);
  grid-template-rows: repeat(8, 1fr);
  border-radius: 1%;
  overflow: hidden;
  background-color: orangered;
}

.square {
  position: relative;
  cursor: pointer;
  transition: opacity 0.4s;
}

.square.dark {
  background-color: var(--color-dark-square);
}

.square.light {
  background-color: var(--color-light-square);
}

.square.light::before,
.square.light::after {
  color: var(--color-dark-square);
}

.square.dark::before,
.square.dark::after {
  color: var(--color-light-square);
}

.square.selected {
  opacity: 0.5;
}

.square[data-rank="1"] {
  grid-row-start: 8;
  grid-row-end: 9;
}

.square[data-rank="1"]::after {
  content: attr(data-file);
  position: absolute;
  bottom: 0;
  right: 8px;
}

.square[data-rank="2"] {
  grid-row-start: 7;
  grid-row-end: 8;
}

.square[data-rank="3"] {
  grid-row-start: 6;
  grid-row-end: 7;
}

.square[data-rank="4"] {
  grid-row-start: 5;
  grid-row-end: 6;
}

.square[data-rank="5"] {
  grid-row-start: 4;
  grid-row-end: 5;
}

.square[data-rank="6"] {
  grid-row-start: 3;
  grid-row-end: 4;
}

.square[data-rank="7"] {
  grid-row-start: 2;
  grid-row-end: 3;
}

.square[data-rank="8"] {
  grid-row-start: 1;
  grid-row-end: 2;
}

.square[data-file="a"] {
  grid-column-start: 1;
  grid-column-end: 2;
}

.square[data-file="a"]::before {
  content: attr(data-rank);
  position: absolute;
  top: 4px;
  left: 8px;
}

.square[data-file="b"] {
  grid-column-start: 2;
  grid-column-end: 3;
}

.square[data-file="c"] {
  grid-column-start: 3;
  grid-column-end: 4;
}

.square[data-file="d"] {
  grid-column-start: 4;
  grid-column-end: 5;
}

.square[data-file="e"] {
  grid-column-start: 5;
  grid-column-end: 6;
}

.square[data-file="f"] {
  grid-column-start: 6;
  grid-column-end: 7;
}

.square[data-file="g"] {
  grid-column-start: 7;
  grid-column-end: 8;
}

.square[data-file="h"] {
  grid-column-start: 8;
  grid-column-end: 9;
}

.arrow {
  position: absolute;
  top: 0;
  bottom: 0;
  width: 100%;
}

@media (max-width: 600px) {
  .square[data-file="a"]::before {
    content: none;
  }

  .square[data-rank="1"]::after {
    content: none;
  }
}
</style>

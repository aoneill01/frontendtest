<script setup>
import { computed } from "vue";

const props = defineProps(["from", "to"]);

const location = (start, distance, angle) => ({
  x: distance * Math.cos(angle) + start.x,
  y: distance * Math.sin(angle) + start.y,
});

const toPair = (p) => `${p.x} ${p.y}`;

const toLocalSpace = ({ rank, file }) => ({
  x: file.charCodeAt(0) - "a".charCodeAt(0) + 0.5,
  y: 8.5 - rank,
});

const calculateD = () => {
  if (!props.from || !props.to) return "";

  const thickness = 0.18;
  const start = toLocalSpace(props.from);
  const end = toLocalSpace(props.to);

  if (start.x === end.x && start.y === end.y) return "";

  const angle = Math.atan2(end.y - start.y, end.x - start.x);

  const p1 = location(start, 0.3, angle);
  const p2 = location(end, thickness * 2, angle + Math.PI);

  return `
    M ${toPair(location(p1, thickness, angle + Math.PI / 2))}
    L ${toPair(location(p2, thickness, angle + Math.PI / 2))}
    L ${toPair(location(p2, 2 * thickness, angle + Math.PI / 2))}
    L ${toPair(location(p2, thickness * 2, angle))}
    L ${toPair(location(p2, 2 * thickness, angle - Math.PI / 2))}
    L ${toPair(location(p2, thickness, angle - Math.PI / 2))}
    L ${toPair(location(p1, thickness, angle - Math.PI / 2))}
    Z`;
};

const d = computed(calculateD);
</script>

<template>
  <svg viewBox="0 0 8 8" xmlns="http://www.w3.org/2000/svg">
    <path :d="d" fill="rgb(84, 32, 192)" />
  </svg>
</template>

<style scoped>
svg {
  pointer-events: none;
}
</style>

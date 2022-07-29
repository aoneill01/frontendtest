<script setup>
const props = defineProps(["history"]);
</script>

<template>
  <nav>
    <h2>Selected Squares</h2>
    <ol>
      <li v-for="(square, i) in props.history" :key="i">
        {{ square.file }}{{ square.rank }}
      </li>
    </ol>
  </nav>
</template>

<style scoped>
nav {
  min-width: 200px;
  background-color: var(--color-background-alt);
  border-radius: 5px;
  padding: 8px 16px;
}

h2 {
  font-weight: bold;
  font-size: 20px;
  margin-bottom: 8px;
  text-align: center;
}

li::marker {
  color: hsla(0, 0%, 100%, 0.4);
}

@media (max-width: 480px) {
  ol {
    display: flex;
    flex-wrap: wrap;
  }
  ol > li {
    margin-right: 36px;
    width: 30px;
  }
}
</style>

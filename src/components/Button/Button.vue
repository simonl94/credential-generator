<script setup>
defineProps({
  msg: {
    type: String,
    required: true,
  },
});
</script>

<template>
  <button class="button">
    <slot />
  </button>
</template>

<style scoped>
.button {
  display: inline-block;
  margin: 0.5em 0;
  padding: 1em 2em;
  background: #42b883;
  border: 2px solid black;
  border-radius: 10px;
  color: rgba(255, 255, 255, 0.87);
  font-family: 'Quicksand', sans-serif;
  font-size: 1em;
  font-weight: 700;
  letter-spacing: 0.02em;
  line-height: 1;
  text-decoration: none;
  text-transform: uppercase;
  cursor: pointer;
  transition: 0.3s;
}

.button:hover {
  background: #36815f;
  color: #fff;
}

.button:disabled {
  cursor: not-allowed;
}
</style>

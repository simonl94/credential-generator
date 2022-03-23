<script setup>
import Button from '../Button/Button.vue';
import { ref } from 'vue';
import * as Vue from 'vue';
import axios from 'axios';

let name = ref('Please generate a name');
let disabled = ref(false);
function generateName() {
  disabled.value = true;
  axios
    .get('https://randomuser.me/api/?nat=us,gb,au&inc=name')
    .then((response) => {
      name.value =
        response.data.results[0].name.first +
        ' ' +
        response.data.results[0].name.last;
      disabled.value = false;
    });
}
</script>

<template>
  <main>
    <div class="card">
      <p class="name">
        {{ name }}
      </p>

      <div class="generateName">
        <Button @click="generateName" :disabled="disabled">Generate</Button>
      </div>
    </div>
  </main>
</template>

<style scoped>
.card {
  width: 320px;
  height: auto;
  min-height: 250px;
  background: rgb(60, 62, 68);
  border-radius: 20px;
  overflow: hidden;
  padding: 10px 15px;
  margin-bottom: 24px;
  margin-right: 10px;
  transition: all 0.2s linear;
  color: white;
}

.name {
  display: flex;
  justify-content: center;
}

.generateName {
  display: flex;
  justify-content: center;
  margin-top: 143px;
}
</style>

<script setup>
import Button from '../Button/Button.vue';
import { ref } from 'vue';
import * as Vue from 'vue';
import axios from 'axios';

//Declare variable initial states
let displayName = ref('Please generate a name');
let displayUsername = ref('');
let displayPassword = ref('');
let disableNameButton = ref(false);
let disableCredentialButton = ref(true);
let showCreds = ref(false);

//Function to generate a first and last name
function generateName() {
  disableNameButton.value = true;
  disableCredentialButton.value = true;
  displayUsername.value = '';
  displayPassword.value = '';
  //API that fetches names with specific rules e.g. nat=us
  axios
    .get('https://randomuser.me/api/?nat=us,gb,au&inc=name')
    .then((response) => {
      displayName.value =
        response.data.results[0].name.first +
        ' ' +
        response.data.results[0].name.last;
      disableNameButton.value = false;
      disableCredentialButton.value = false;
    })
    .catch((error) => {
      //Catch any errors and let the user know by setting the displayName
      displayName.value = 'Error occurred! Please try again';
      console.log(error);
      disableNameButton.value = false;
      disableCredentialButton.value = true;
    });
}

function generateCredentials() {
  showCreds.value = true;
  displayPassword.value = '';
  const passwordOptions =
    'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789!#$%&?@';

  for (let i = 0; i < 7; i++) {
    displayPassword.value +=
      passwordOptions[Math.floor(Math.random() * passwordOptions.length)];
  }

  //Get the current displayName value and split the names
  var splitName = displayName.value.split(' ');
  //Get the first name from the new splitName array and create a username
  displayUsername.value =
    splitName[0].charAt(0).toLowerCase() + '.' + splitName[1].toLowerCase();
}
</script>

<template>
  <main>
    <div class="card">
      <p class="name">
        {{ displayName }}
      </p>
      <div class="generateName">
        <Button @click="generateName" :disabled="disableNameButton"
          >Generate Name</Button
        >
      </div>
      <div v-if="showCreds">
        <p class="username">{{ displayUsername }}</p>

        <p class="password">
          {{ displayPassword }}
        </p>
      </div>
      <div class="generateCredentials">
        <Button @click="generateCredentials" :disabled="disableCredentialButton"
          >Generate Credentials</Button
        >
      </div>
    </div>
  </main>
</template>

<style scoped>
.card {
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
}

.generateCredentials {
  display: flex;
  justify-content: center;
}
</style>

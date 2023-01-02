<script setup>
import Input from "./components/Input.vue";
import axios from "axios";
import { ref } from "vue";

const word = ref();
const screen = ref();

async function getData(word) {
  const result = await axios(
    `https://api.dictionaryapi.dev/api/v2/entries/en/${word}`
  ).then(
    (response) => (screen.value = response.data[0].meanings[0].definitions[0].definition)
  );

  return result;
}

const clickHandler = async () => {
  try {
    await getData(word.value);
  } catch (e) {
    screen.value = "404 - Data not found. Please try again.";
    console.error(e);
  }
};
</script>

<template>
  <div class="container">
    <p>{{ screen }}</p>
    <img src="./assets/snowman.png" alt="">
    <Input v-model:word="word" placeholder="Enter a word"></Input>
    <button @click="clickHandler">Submit</button>
  </div>
</template>

<style>

.container {
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
  font-size: 24px;
  width: 100%;
  height: 100%;
  background: aqua;
  display: flex;
  justify-content: center;
  align-items: center;
}

button{
  width: 100px;
  padding: 15px;
  border-radius: 15px;
  border: none;
  margin: 0px 10px 30px 10px;
  background-color: purple;
  color: white;
  cursor: pointer;
  font-size: 16px;
}

p{
  position: absolute;
  left: 48%;
  top: 65%;
  transform: translate(-50%, -50%);
  font-size: 48px;
}

img{
  position: absolute;
  left: 47.1%;
  top: 36%;
  z-index: -1;
  transform: translate(-50%, -50%);
  width: 550px;

}
</style>

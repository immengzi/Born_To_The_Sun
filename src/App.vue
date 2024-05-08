<script setup>
import quotes from './quotes.json';
import {onBeforeUnmount, onMounted, ref} from "vue";

let quote = ref(getQuote());

function getQuote() {
  let randomIndex = Math.floor(Math.random() * quotes.length);
  let quoteText = quotes[randomIndex].quote;
  return quoteText.replace(/\n/g, '<br>');
}

let intervalId;
onMounted(() => {
  intervalId = setInterval(() => {
    quote.value = getQuote();
  }, 3000);
});

onBeforeUnmount(() => {
  clearInterval(intervalId);
});
</script>

<template>
  <div id="app">
    <div class="container">
      <div class="quote" v-html="quote"></div>
      <audio controls="controls" class="player">
        <source src="https://file.mengzi.li/%E5%90%91%E9%98%B3%E8%80%8C%E7%94%9F_%E6%97%A5%E5%87%BA_live.mp3" type="audio/mp3" />
      </audio>
    </div>
  </div>
</template>

<style scoped>
#app {
  height: 100vh;
  width: 100vw;
  position: fixed;
  background-image: linear-gradient(rgb(229, 205, 176), rgb(198, 78, 73));
  display: flex;
  justify-content: center;
  align-items: center;
}

.quote {
  font-size: 2rem;
  font-family: 汇文明朝体;
  text-align: center;
  color:rgba(255,255,255,0.9);
}

.player {
  position: fixed;
  bottom: 3rem;
  left: 50%;
  transform: translateX(-50%);
}
</style>

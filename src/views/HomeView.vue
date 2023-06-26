<template>
  <main class="home">
    <div>
      <h1>Tu é brabo?</h1>
      <h2>Bora ver, dá o play aí.</h2>
      <button v-on:click="start()" v-bind:disabled="isPlaying">Play</button>
      <Block v-if="isPlaying" v-bind:delay="delay" @end="endGame" />
      <Result v-if="showResults" v-bind:score="score" />
    </div>
  </main>
</template>

<script>
import { ref } from "vue";
import Block from "../components/Block.vue";
import Result from "../components/Result.vue";
export default {
  components: {
    Block,
    Result,
  },
  setup() {
    const isPlaying = ref(false);
    const delay = ref(0);
    const score = ref(0);
    const showResults = ref(false);

    const start = () => {
      delay.value = 2000 + Math.random() * 5000;
      isPlaying.value = true;
      showResults.value = false;
    };

    const endGame = (reactionTime) => {
      score.value = reactionTime._value;
      isPlaying.value = false;
      showResults.value = true;
    };

    return {
      isPlaying,
      delay,
      start,
      endGame,
      score,
      showResults,
    };
  },
};
</script>

<style scoped>
.home {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  text-align: center;
  width: 100vw;
  height: 100vh;
  background-color: #0b6951;
  color: #fff;
}

button {
  background: #0faf87;
  color: #fff;
  border: none;
  padding: 8px 16px;
  border-radius: 4px;
  font-size: 16px;
  letter-spacing: 1px;
  cursor: pointer;
  margin: 8px;
}

button[disabled] {
  opacity: 0.2;
  cursor: not-allowed;
}
</style>

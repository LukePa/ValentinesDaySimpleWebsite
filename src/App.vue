<script setup>
  import {ref, computed} from "vue";
  import NoButton from "./components/NoButton.vue";


  const left = ref(null);
  const top = ref(null);
  const racoonSpeech = ref(null);

  const randomRacoonPhrases = [
    "No! Please just say yes!",
    "I'll keep doing this forever",
    "I'm not gonna take no for an answer here",
    "...",
    "Come on, there's no need for this",
    "I promise, I'll tell Luke to stop putting phildelpia in carbonara",
    "Why would you keep chasing me :(",
    "Please stop",
    "There are two more buttons for you to press",
    "You're not gonna be pressing this button"
  ]

  const getRandomRacoonSpeech = () => {
    return randomRacoonPhrases[Math.floor(Math.random() * randomRacoonPhrases.length)]
  }

  const setRacoonSpeech = () => {
    console.log("caled")
    if (!racoonSpeech.value) {
      racoonSpeech.value = "Cool, I'll just take this then if you're gonna be like that";
    }
    else {
      racoonSpeech.value = getRandomRacoonSpeech()
    };
  }

  const run = () => {
    const leftNumber = Math.floor(Math.random() * (90))
    const topNumber = Math.floor(Math.random() * (90))

    left.value = `${leftNumber}%`;
    top.value = `${topNumber}%`;
    setRacoonSpeech();
  }

  const isRunning = computed(() => {
    return left.value !== null && top.value !== null;
  })

  const clearRunning = () => {
    left.value = null;
    top.value = null;
    racoonSpeech.value = null;
  }


  const response = ref(null);

  const responseNotPositive = computed(() => {
    return !(response.value === "sass" || response.value === "sweet");
  });

  const setResponse = (string) => {
    if (!['sass', 'sweet'].includes(string)) throw new Error("Invalid response given");
    clearRunning();
    response.value = string;
  }

  const clearResponse = () => {
    response.value = null;
  }
</script>

<template>
  <div class="page-container">
    <div v-if="responseNotPositive">
      <h1>Dalila, Will You Be My Valentine?</h1>
      <div class="button-section">
        <button class="positive" @click="setResponse('sass')">Errr, obviously? You are my boyfriend?</button>
        <button class="positive" @click="setResponse('sweet')">Of course Luke! I'd absolutely love to!</button>
        <NoButton :class="{running: isRunning}" @click="run" :racoonSpeech="racoonSpeech">Sorry, but it's a no....</NoButton>
      </div>
    </div>

    <div v-else-if="response === 'sass'" class="accept-container">
      <h2>Thank you I really appreciate that, it makes me really happy 🥺</h2>
      <h3>But was the sass really needed?</h3>
      <button @click="clearResponse">Choose another option</button>
    </div>

    <div v-else-if="response === 'sweet'" class="accept-container">
      <h2>Thank you! That is so sweet</h2>
      <h3>I love you, and I can't wait to see you tomorrow (I might even wear a shirt for you now)</h3>
      <button @click="clearResponse">Choose another option</button>
    </div>
  </div>
</template>

<style scoped>
  .page-container {
    flex: 1;
    background-image: url("/heart-background.jpg");
    background-repeat: no-repeat;
    background-size: cover;
  }

  h1 {
    text-align: center;
    padding: 60px 0;
    margin: 0;
    text-decoration: underline;
  }

  .button-section {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    grid-template-rows: 1fr;
    gap: 40px;
    margin: 0 40px;
  }

  .positive {
    background: #368E0F;
  }

  .negative {
    background: #FA0026;
  }

  .running {
    position: absolute;
    left: v-bind(left);
    top: v-bind(top);
  }

  button {
    padding: 20px;
    border: none;
    border-radius: 20px;
    font-size: 20px;
    transition: all 0.25s ease-in-out;
    background: #E0115F
  }

  button:hover {
    background: black;
    color: white;
    cursor: pointer;
  }

  .accept-container {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    text-align: center;
    padding-top: 100px;
    gap: 50px;

  }

  @media (max-width: 742px) {
    .button-section {
      grid-template-columns: 1fr;
      grid-template-rows: 1fr 1fr 1fr;
    }
  }
</style>

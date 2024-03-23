<template>
  <div class="wrapper">
    <h1>Clicker Speed Test NEFORWARD</h1>
    <p>You will be clicking for {{ time }} seconds</p>
    <button @click="forwardInDaHouse" v-if="isStopped">Start</button>
    <div @click="increment" class="start" v-if="!isStopped">
      {{ counter }}
    </div>

    <div class="settings">
      <input type="text" placeholder="Enter seconds" v-model="time" />
    </div>

    <div class="history-book">
      <ul>
        <li v-for="session in history" :key="session.id">
          <span> {{ session.score + " times" }}</span>
          <br />
          <span> {{ session.duration }} seconds</span>
        </li>
      </ul>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";

const time = ref(5);

const counter = ref(0);

const isStopped = ref(true);

const history = ref([]);

const increment = () => {
  if (!isStopped.value) {
    counter.value++;
  }
};

const forwardInDaHouse = () => {
  isStopped.value = false;
  counter.value = 0;

  const startTime = Date.now();

  setTimeout(() => {
    isStopped.value = true;
    const endTime = Date.now();
    const duration = (endTime - startTime) / 1000;

    history.value.push({
      id: Date.now(),
      score: counter.value,
      duration: duration.toFixed(2),
    });
  }, time.value * 1000);
};
</script>

<style lang="scss">
.wrapper {
  max-width: 800px;
  margin: 0 auto;
  background: #999;
  border-radius: 20px;
  height: 90vh;
  width: 80vw;
  padding: 20px;
  box-sizing: border-box;
}
body {
  background: #000;
  margin: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100vh;
  font-family: "Courier New", Courier, monospace;
}
h1 {
  text-align: center;
}
.start {
  width: 100%;
  height: 200px;
  background: #ccc;
  border: none;
  font-size: 40px;
  display: flex;
  justify-content: center;
  align-items: center;
}
button {
  background: lightblue;
  border: none;
  font-size: 20px;
}
.history-book {
  ul {
    li {
      margin-bottom: 20px;
      list-style: none;
    }
  }
}
</style>

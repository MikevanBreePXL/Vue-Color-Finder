<script setup>
import {ref} from "vue";

let hexCode = ref("Start moving!");

function mouseEpilepsy(event) {
  document.body.style.backgroundColor = "#" + (2 * event.clientX * event.clientY);
}

function mouseTracker(event) {
  let redValue = Math.round((visualViewport.width - event.clientX) / visualViewport.width * 255 - (event.clientY / visualViewport.height * 255));
  redValue = redValue < 0 ? 0 : redValue;
  let blueValue = Math.round(event.clientX / visualViewport.width * 255 - (event.clientY / visualViewport.height * 255));
  blueValue = blueValue < 0 ? 0 : blueValue;
  let greenValue = Math.round(event.clientY / visualViewport.height * 255);
  greenValue = greenValue < 0 ? 0 : greenValue;
  let rgbCode = "rgb(" + redValue + ", " + greenValue + ", " + blueValue + ")";

  hexCode = "#" + redValue.toString(16) + greenValue.toString(16) + blueValue.toString(16);
  //document.body.style.backgroundColor = rgbCode;
  document.getElementById("mainText").textContent = rgbCode;
  document.body.style.backgroundColor = rgbCode;
}
</script>

<template>
  <main class="main" v-on:mousemove="mouseTracker">
    <h1 id="mainText">{{ hexCode }}</h1>
    <span id="vueText"><img src="./assets/logo.svg" style="height: 1em;"  alt="Vue logo"/> Powered by Vue.Js</span>
  </main>
</template>

<style scoped>
* {
  margin: 0;
  padding: 0;
  font-family: 'Montserrat Medium', sans-serif;
  color: #ADADAD;
}

.main {
  display: flex;
  height: 98vh;
  width: 100%;
}

#mainText {
  font-size: 2em;
  align-self: center;
  margin: 0 auto;
}
#vueText {
  align-self: flex-end;
}
</style>
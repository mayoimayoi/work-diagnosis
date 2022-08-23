<script setup>
import { ref } from "vue";
let count = 0;
let status = 0;
const quesiton = ref("転職度診断");
const result = ref("");
const selectBtn = ref(false);
const startBtn = ref(true);
const retryBtn = ref(false);

const questionBox = [
  "毎日定時に帰れる仕事がしたい",
  "尊敬できる上司の下で働きたい",
  "手当や福利厚生が充実している会社で働きたい",
  "転勤のない仕事がしたい",
];
// スタートボタンを押した時の動作
const startDiagnosis = () => {
  count = 0;
  startBtn.value = !startBtn.value;
  selectBtn.value = !selectBtn.value;
  quesiton.value = questionBox[count];
};

const retryDiagnosis = () => {
  quesiton.value = "転職度診断";
  result.value = "";
  startBtn.value = !startBtn.value;
  retryBtn.value = !retryBtn.value;
};

const nextQestion = (answer) => {
  if (answer == "Yes") {
    status++;
  }

  count++;
  if (count == questionBox.length) {
    quesiton.value = "終了です";
    const safePercent = (status / questionBox.length) * 100;
    result.value = "あなたの安心したい度は" + safePercent + "%です。";
    retryBtn.value = !retryBtn.value;
    selectBtn.value = !selectBtn.value;
  } else {
    quesiton.value = questionBox[count];
  }
};
</script>

<template>
  <div>
    <p>{{ quesiton }}</p>
    <p>{{ result }}</p>
    <div v-show="startBtn">
      <button @click="startDiagnosis">スタート</button>
    </div>
    <div v-show="selectBtn">
      <button @click="nextQestion('Yes')">はい</button>
      <button @click="nextQestion('No')">いいえ</button>
    </div>
    <div v-show="retryBtn">
      <button @click="retryDiagnosis">リトライ</button>
    </div>
  </div>
</template>

<style scoped></style>

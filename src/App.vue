<script setup>
import { ref } from "vue";
import backImg from "./assets/top.jpg";

let count = 0;
let status = 0;
const quesiton = ref("あなたの転職したい度を診断します");
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
  status = 0;
  startBtn.value = !startBtn.value;
  selectBtn.value = !selectBtn.value;
  quesiton.value = questionBox[count];
};

// リトライボタンを押した時の操作
const retryDiagnosis = () => {
  quesiton.value = "あなたの転職したい度を診断します";
  result.value = "";
  startBtn.value = !startBtn.value;
  retryBtn.value = !retryBtn.value;
};

// はいかいいえを押した時の操作
const nextQestion = (answer) => {
  if (answer == "Yes") {
    status++;
  }

  count++;
  if (count == questionBox.length) {
    quesiton.value = "お疲れ様でした！";
    const safePercent = (status / questionBox.length) * 100;
    result.value = "あなたの転職したい度は" + safePercent + "%です。";
    retryBtn.value = !retryBtn.value;
    selectBtn.value = !selectBtn.value;
  } else {
    quesiton.value = questionBox[count];
  }
};
const test2 = () => {
  console.log("ttt");
  document.getElementById("test").src = backImg;
};
</script>

<template>
  <div class="mainbox">
    <h1>転職度診断</h1>
    <div class="quesitonbox">
      <p>{{ quesiton }}</p>
      <p>{{ result }}</p>
    </div>
    <div v-show="startBtn">
      <button class="btn blue" @click="startDiagnosis">スタート</button>
    </div>
    <div v-show="selectBtn">
      <button class="btn whiteblue" @click="nextQestion('Yes')">はい</button>
      <button class="btn red" @click="nextQestion('No')">いいえ</button>
    </div>
    <div v-show="retryBtn">
      <p>あなたの転職イメージ</p>
      <img :src="backImg" alt="転職イメージ画像" class="resultimg" />
      <button class="btn red" @click="retryDiagnosis">リトライ</button>
    </div>
  </div>
</template>

<style scoped>
@import "assets/css/reset.css";

.mainbox {
  width: 80%;
  margin: 0 auto;
  padding: 20px 30px;
  background: #ffffee;
  box-shadow: 0px 0px 0px 10px #ffffbb;
  border: dashed 2px white;
}
.mainbox p {
  margin: 0;
  padding: 0;
}
.quesitonbox {
  margin: 2em 0;
  position: relative;
  padding: 20px 10px;
  border: solid 2px #ffcb8a;
  border-radius: 3px 0 3px 0;
}
.quesitonbox:before,
.quesitonbox:after {
  content: "";
  position: absolute;
  width: 10px;
  height: 10px;
  border: solid 2px #ffcb8a;
  border-radius: 50%;
}
.quesitonbox:after {
  top: -12px;
  left: -12px;
}
.quesitonbox:before {
  bottom: -12px;
  right: -12px;
}
.quesitonbox p {
  margin: 0;
  padding: 0;
}
.btn {
  padding: 10px 30px;
  margin: 10px 30px;
}
.blue {
  background-color: aqua;
}
.whiteblue {
  background-color: deepskyblue;
}
.red {
  background-color: indianred;
}
.resultimg {
  margin: 0 auto;
  width: 50%;
}
</style>

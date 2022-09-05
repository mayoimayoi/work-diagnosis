<script setup>
import { ref } from "vue";
import accountantImg from "./assets/accountant.jpg";
import actorImg from "./assets/actor.jpg";
import engineerImg from "./assets/engineer.jpg";
import salesImg from "./assets/sales.jpg";
import trainerImg from "./assets/trainer.jpg";

// 変数へ初期値を代入
const questionBox = [
  "あなたの天職を診断します",
  "好きな色は?",
  "好きなのは?",
  "どちらの作業が得意?",
  "休日行くとしたら?",
  "リーダーのような役職は?",
  "もし結婚するとしたら?",
  "絵を描くのは得意な方だ",
  "展示会など人に見られる仕事が好き",
  "つい部屋の模様替えをしてしまう",
  "服のセンスはあると思う",
  "休みの日は?",
  "プレゼンで人を説得するのが得意",
  "服装にはこだわりがある",
  "PCを使う作業は得意",
  "人と話すのが好き",
  "物作りが好き",
];
const yesBox = [
  "始める",
  "明るい色",
  "大勢でいる方",
  "コツコツ細かい作業",
  "山",
  "好き",
  "スタイルの良い俳優",
  "はい",
  "はい",
  "はい",
  "はい",
  "外で過ごす",
  "はい",
  "はい",
  "はい",
  "はい",
  "はい",
];
const noBox = [
  "",
  "落ち着いた色",
  "少人数でいる方",
  "大きな決断をする作業",
  "海",
  "苦手",
  "知的な医学関係者",
  "いいえ",
  "いいえ",
  "いいえ",
  "いいえ",
  "部屋で過ごす",
  "いいえ",
  "いいえ",
  "いいえ",
  "いいえ",
  "いいえ",
];
const resultBox = [
  "",
  "演技系",
  "事務・経理系",
  "営業系",
  "エンジニア系",
  "体力系",
];
let questionNumber = 0;
const quesitonContent = ref(questionBox[0]);
const yesSelect = ref(yesBox[0]);
const noSelect = ref("");
const resultContent = ref("");
const selectBtn = ref(false);
const startBtn = ref(true);
const retryBtn = ref(false);
const trainerShow = ref(false);
const salesShow = ref(false);
const engineerShow = ref(false);
const actorShow = ref(false);
const accountantShow = ref(false);

// スタートボタンを押した時の動作
const startDiagnosis = () => {
  questionNumber = 1;
  startBtn.value = !startBtn.value;
  selectBtn.value = !selectBtn.value;
  quesitonContent.value = questionBox[questionNumber];
  yesSelect.value = yesBox[questionNumber];
  noSelect.value = noBox[questionNumber];
};

// リトライボタンを押した時の操作
const retryDiagnosis = () => {
  quesitonContent.value = questionBox[0];
  resultContent.value = "";
  startBtn.value = !startBtn.value;
  retryBtn.value = !retryBtn.value;
  trainerShow.value = false;
  salesShow.value = false;
  engineerShow.value = false;
  actorShow.value = false;
  accountantShow.value = false;
};

// 結果を表示する
const resultDiagnosis = (resultNumber) => {
  quesitonContent.value = "あなたの向いている職業は";
  resultContent.value = resultBox[resultNumber];
  selectBtn.value = !selectBtn.value;
  retryBtn.value = !retryBtn.value;
  if (resultNumber == 1) {
    actorShow.value = !actorShow.value;
  } else if (resultNumber == 2) {
    accountantShow.value = !accountantShow.value;
  } else if (resultNumber == 3) {
    salesShow.value = !salesShow.value;
  } else if (resultNumber == 4) {
    engineerShow.value = !engineerShow.value;
  } else {
    trainerShow.value = !trainerShow.value;
  }
};

// はいかいいえを押した時の操作
const nextQestion = (selectAnswer) => {
  if (questionNumber == 1) {
    if (selectAnswer == "Yes") {
      questionNumber = 2;
    } else {
      questionNumber = 4;
    }
  } else if (questionNumber == 2) {
    if (selectAnswer == "Yes") {
      questionNumber = 3;
    } else {
      questionNumber = 5;
    }
  } else if (questionNumber == 3) {
    if (selectAnswer == "Yes") {
      questionNumber = 5;
    } else {
      questionNumber = 6;
    }
  } else if (questionNumber == 4) {
    if (selectAnswer == "Yes") {
      questionNumber = 7;
    } else {
      questionNumber = 5;
    }
  } else if (questionNumber == 5) {
    if (selectAnswer == "Yes") {
      questionNumber = 8;
    } else {
      questionNumber = 7;
    }
  } else if (questionNumber == 6) {
    if (selectAnswer == "Yes") {
      questionNumber = 9;
    } else {
      questionNumber = 8;
    }
  } else if (questionNumber == 7) {
    if (selectAnswer == "Yes") {
      questionNumber = 10;
    } else {
      questionNumber = 11;
    }
  } else if (questionNumber == 8) {
    if (selectAnswer == "Yes") {
      questionNumber = 11;
    } else {
      questionNumber = 7;
    }
  } else if (questionNumber == 9) {
    if (selectAnswer == "Yes") {
      questionNumber = 12;
    } else {
      questionNumber = 8;
    }
  } else if (questionNumber == 10) {
    if (selectAnswer == "Yes") {
      questionNumber = 15;
    } else {
      questionNumber = 14;
    }
  } else if (questionNumber == 11) {
    if (selectAnswer == "Yes") {
      questionNumber = 15;
    } else {
      questionNumber = 16;
    }
  } else if (questionNumber == 12) {
    if (selectAnswer == "Yes") {
      questionNumber = 15;
    } else {
      questionNumber = 16;
    }
  } else if (questionNumber == 13) {
    if (selectAnswer == "Yes") {
      resultDiagnosis(1);
      return;
    } else {
      resultDiagnosis(5);
    }
  } else if (questionNumber == 14) {
    if (selectAnswer == "Yes") {
      resultDiagnosis(2);
      return;
    } else {
      questionNumber = 13;
    }
  } else if (questionNumber == 15) {
    if (selectAnswer == "Yes") {
      resultDiagnosis(3);
      return;
    } else {
      questionNumber = 14;
    }
  } else {
    if (selectAnswer == "Yes") {
      resultDiagnosis(4);
      return;
    } else {
      questionNumber = 13;
    }
  }
  quesitonContent.value = questionBox[questionNumber];
  yesSelect.value = yesBox[questionNumber];
  noSelect.value = noBox[questionNumber];
};
</script>

<template>
  <div class="mainbox">
    <h1>転職度診断</h1>
    <div class="quesitonbox">
      <p>{{ quesitonContent }}</p>
      <p>{{ resultContent }}</p>
    </div>
    <div v-show="startBtn">
      <button class="btn blue" @click="startDiagnosis">スタート</button>
    </div>
    <div v-show="selectBtn">
      <button class="btn whiteblue" @click="nextQestion('Yes')">
        {{ yesSelect }}
      </button>
      <button class="btn red" @click="nextQestion('No')">
        {{ noSelect }}
      </button>
    </div>
    <div v-show="retryBtn">
      <p>あなたの転職イメージ</p>
      <div v-show="accountantShow">
        <img :src="accountantImg" alt="会計士画像" class="resultimg" />
        <a class="weblink" href="https://cpa.mynavi.jp/"
          >転職にチャレンジしてみる</a
        >
      </div>
      <div v-show="engineerShow">
        <img :src="engineerImg" alt="エンジニア画像" class="resultimg" />
        <a class="weblink" href="https://doda.jp/engineer/"
          >転職にチャレンジしてみる</a
        >
      </div>
      <div v-show="actorShow">
        <img :src="actorImg" alt="俳優画像" class="resultimg" /><a
          class="weblink"
          href="https://www.audition-com.net/l/agency-top/"
          >転職にチャレンジしてみる</a
        >
      </div>

      <div v-show="salesShow">
        <img :src="salesImg" alt="営業画像" class="resultimg" /><a
          class="weblink"
          href="https://tenshoku.mynavi.jp/selectjob-11/"
          >転職にチャレンジしてみる</a
        >
      </div>

      <div v-show="trainerShow">
        <img :src="trainerImg" alt="トレーナー画像" class="resultimg" />
        <a class="weblink" href="https://tenshoku.mynavi.jp/list/o1F220/"
          >転職にチャレンジしてみる</a
        >
      </div>
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
.weblink {
  font-size: 24px;
}
</style>

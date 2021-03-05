<template>
  <div class="quiz__header">
    <h2>Quiz {{ quizNum }}</h2>
    <div class="quiz__questCount">
      <p>{{ currQuest }} / {{ totalQuest }}</p>
    </div>
  </div>
  <div class="quiz__quest__box">
    <div class="quiz__quest">
      <div class="num1">
        <p>{{ qNum1 }}</p>
      </div>
      <div class="operator">
        <p>{{ qOper }}</p>
      </div>
      <div class="num2">
        <p>{{ qNum2 }}</p>
      </div>
    </div>
    <div class="quiz__answer">
      <input
        type="text"
        id="answer"
        placeholder="answer"
        required
        v-model="userAnswer"
      />
    </div>
  </div>
  <div class="quiz__score">
    <p>
      Correct Answers: <span style="color: green">{{ correctAnswer }}</span>
    </p>
  </div>
  <div class="quiz__next">
    <a href="#" class="btn" @click="nextQuest">NEXT ➔</a>
  </div>
</template>

<script>
export default {
  name: "quiz-content",
  props: ["totalQuest", "quizNum"],
  data() {
    return {
      num1: 1,
      questions: [],
      qNum1: null,
      qNum2: null,
      qOper: null,
      correctAnswer: 0,
      userAnswer: null,
      currQuest: 1,
    };
  },
  computed: {
    num2() {
      return Number(this.num1) + Number(this.totalQuest);
    },
  },
  methods: {
    nextQuest() {
      if (this.currQuest <= this.totalQuest) {
        let quest = this.qNum1 + " " + this.qOper + " " + this.qNum2;
        let compAnswer = Math.floor(eval(this.qNum1 + this.qOper + this.qNum2));
        let status = false;
        if (
          Number(this.userAnswer) === Number(compAnswer) &&
          this.userAnswer !== null
        ) {
          this.correctAnswer++;
          status = true;
        }
        this.questions.push({
          question: quest,
          userAnswer: this.userAnswer,
          computedAnswer: compAnswer,
          correct: status,
        });
        this.currQuest++;
        this.createQuest();
      }
      if (Number(this.currQuest) > Number(this.totalQuest)) {
        this.quizState = "complete";
        this.$emit("quizoComplete", {
          questions: this.questions,
          correctAnswer: this.correctAnswer,
        });
      }
    },
    createQuest() {
      this.qNum1 = this.randomNum();
      this.qNum2 = this.randomNum();
      this.qOper = this.randomOperator();
      this.userAnswer = null;
    },
    randomNum() {
      return Math.floor(
        Math.random() * (Number(this.num2) - Number(this.num1) + 1) +
          Number(this.num1)
      );
    },
    randomOperator() {
      let operator = ["+", "-", "/", "*"];
      let random = Math.floor(Math.random() * 3);
      return operator[random];
    },
  },
  created() {
    console.log("created");
    this.createQuest();
  },
};
</script>

<style scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: Arial, Helvetica, sans-serif;
}

.quiz__content {
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}
.quiz__header {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  padding: 1rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
  background-color: teal;
  color: #fff;
  box-shadow: 0 5px 8px darkgrey;
}

.quiz__quest__box {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.quiz__quest {
  width: 200px;
  display: flex;
  justify-content: space-between;
  border: 1px solid green;
  padding: 1rem 2rem;
  font-weight: bold;
  font-size: 1.2rem;
}

.num1,
.num2 {
  color: blue;
}

.operator {
  color: red;
}

.quiz__answer {
  margin: 1rem;
}

.quiz__answer input {
  font-size: 1.1rem;
  width: 100px;
  padding: 1rem;
  display: block;
}

.quiz__next {
  position: absolute;
  bottom: 10px;
  right: 10px;
}

.quiz__score {
  position: absolute;
  bottom: 30px;
  left: 10px;
  font-size: 1.2rem;
  color: darkblue;
  font-weight: bolder;
}

.btn {
  background-color: darkorange;
  font-weight: bold;
  color: #fff;
  box-shadow: 2px 5px 5px darkgrey;
  padding: 0.6rem 1.2rem;
  text-decoration: none;
  margin: 1rem;
  display: inline-block;
}

.btn:hover {
  transform: translateY(2px);
}
</style>

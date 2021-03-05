<template>
  <div class="quiz__box">
    <div v-if="quizState === 'not-started'" class="quiz__start">
      <quizInit @startQuiz="startQuiz"></quizInit>
    </div>
    <div v-else-if="quizState === 'started'" class="quiz__content">
      <quizContent
        :totalQuest="totalQuest"
        :quizNum="quizNum"
        @quizoComplete="quizoComplete"
      ></quizContent>
    </div>
    <div v-else class="quiz__results">
      <quizResult
        :questions="questions"
        :totalQuest="totalQuest"
        :correctAnswer="correctAnswer"
        :quizNum="quizNum"
      ></quizResult>
    </div>
  </div>
</template>

<script>
import quizInit from "@/components/sub-components/quiz-init.vue";
import quizResult from "@/components/sub-components/quiz-result.vue";
import quizContent from "@/components/sub-components/quiz-content.vue";
export default {
  name: "quiz",
  components: {
    quizInit,
    quizResult,
    quizContent,
  },
  props: ["quizNum"],
  data() {
    return {
      totalQuest: 20,
      correctAnswer: 0,
      questions: [],
      quizState: "not-started",
    };
  },

  methods: {
    startQuiz(data) {
      this.num1 = data.num1;
      this.totalQuest = data.totalQuest;
      this.quizState = "started";
      this.createQuest();
    },
    quizoComplete(data) {
      this.quizState = "complete";
      this.questions = data.questions;
      this.correctAnswer = data.correctAnswer;
    },
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
.quiz__box {
  width: 45%;
  height: 400px;
  position: relative;
  box-shadow: 5px 10px 10px darkgray;
  outline: 1px solid black;
}

.quiz__start {
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.quiz__content {
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}

.quiz__results {
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 1rem;
  padding-top: 5rem;
  border: 1px solid darkcyan;
}
</style>

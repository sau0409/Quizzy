<template>
  <div class="quiz__header">
    <h2>Quiz {{ quizNum }}</h2>
    <p>{{ correctPer }} % Corr Ans</p>
    <div class="quiz__questCount">
      <p>Total Quest: {{ totalQuest }}</p>
      <p>Correct Answ: {{ correctAnswer }}</p>
    </div>
  </div>

  <div class="quiz__detailed">
    <ul>
      <li
        v-for="(q, i) in questions"
        :key="i"
        :class="{ correctClass: q.correct, incoorectClass: !q.correct }"
      >
        Qn: {{ q.question }} User : {{ q.userAnswer }} Exp:
        {{ q.computedAnswer }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "quiz-results",
  props: ["questions", "totalQuest", "correctAnswer", "quizNum"],
  data() {
    return {};
  },
  computed: {
    correctPer() {
      return (Number(this.correctAnswer) / Number(this.totalQuest)) * 100;
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


.quiz__detailed {
  border: 1px solid darkcyan;
  width: 100%;
  height: 100%;
}

.quiz__detailed ul {
  overflow-y: auto;
  height: 300px;
}

.quiz__detailed ul li {
  list-style: none;
  padding: 1rem;
  margin: 0.5rem;
  box-shadow: 0 2px 4px darkgray;
}

.correctClass {
  border: 2px solid green;
}

.incoorectClass {
  border: 2px solid red;
}
</style>


<template>
  <div class="home">
    <div class="quiz__container">
      <Quiz v-for="(q, n) in quizes" :key="n" :quizNum="n+1"></Quiz>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import Quiz from "@/components/quiz.vue";

export default {
  name: "Home",
  components: {
    Quiz,
  },
  data() {
    return {
      quizes: 2
    }
  }
};
</script>


<style scoped>
.quiz__container {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1.5rem;
  height: 100vh;
}
</style>
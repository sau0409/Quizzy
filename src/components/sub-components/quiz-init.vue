<template>
  <div class="quiz__init">
    <div class="quiz__init_number">
      <p>Select A Number :</p>
      <div class="quiz__num1">
        <input type="number" id="num1" v-model="num1" min="1" max="50" />
      </div>
    </div>
    <div class="quiz__init_quest">
      <p>Select Number Of Questions :</p>
      <div class="quiz__questCount">
        <input
          type="number"
          id="questCount"
          v-model="totalQuest"
          min="1"
          max="50"
        />
      </div>
    </div>
  </div>
  <a href="#" class="btn" @click="startingQuiz">Start Quiz ➤</a>
</template>

<script>
export default {
  name: "quiz-init",
  data() {
    return {
      num1: 1,
      totalQuest: 20,
    };
  },

  computed: {
    num2() {
      return Number(this.num1) + Number(this.totalQuest);
    },
  },

  methods: {
    startingQuiz() {
      console.log("emmiting");
      this.$emit("startQuiz", {
        num1: this.num1,
        totalQuest: this.totalQuest,
      });
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

.quiz__start {
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.quiz__init {
  margin-bottom: 5vh;
  width: 100%;
  display: flex;
  justify-content: center;
  flex-direction: column;
  align-items: center;
}

.quiz__init_number,
.quiz__init_quest {
  display: flex;
  justify-content: space-around;
  width: 100%;
  font-weight: 600;
  padding: 1rem;
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

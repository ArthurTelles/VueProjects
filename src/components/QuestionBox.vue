<template>
  <div class="question-box-container">
    <b-jumbotron>
      <template slot="lead">{{ currentQuestion.question }}</template>

      <hr class="my-4" />

      <b-list-group>
        <b-list-group-item
          v-for="(answer, index) in answers"
          :key="index"
          @click="selected(index)"
          :class="[selectedAnswer === index && answered === false ? 'selected' :
          index === 3  && answered === true ? 'correct' : 
          selectedAnswer === index && index != 3  && answered === true ? 'incorrect' : '']"
        >{{ answer }}</b-list-group-item>
      </b-list-group>

      <br />

      <b-button
      @click="submit"
      variant="primary"
      :disabled="this.selectedAnswer === null || this.answered">
        Submit
      </b-button>

      <b-button 
      @click="next();disableSubmit()"
      variant="success">
        Next
      </b-button>
    </b-jumbotron>
  </div>
</template>

<script>
export default {
  data() {
    return {
      selectedAnswer: null,
      answered: false
    };
  },
  props: {
    currentQuestion: Object,
    next: Function
  },
  methods: {
    selected(index) {
      this.selectedAnswer = index;
    },
    submit() {
      this.answered = true;
    },
    disableSubmit() {
      this.answered = false;
      this.selectedAnswer = null;
    }
  },
  computed: {
    answers() {
      this.answered = false;
      let answers = [...this.currentQuestion.incorrect_answers];
      answers.push(this.currentQuestion.correct_answer);
      return answers;
    }
  }
};
</script>

<style scoped>
.btn {
  margin: 0 1%;
}

.list-group-item:hover {
  background: lightgray;
  cursor: pointer;
}

.selected {
  background-color: lightblue;
}

.correct {
  background-color: lightgreen;
}

.incorrect {
  background-color: lightcoral;
}
</style>

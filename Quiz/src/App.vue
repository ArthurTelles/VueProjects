<template>
  <div id="app">
    <Header v-if="this.questions.length > 0"
      :currentQuestionNumber="this.index+1"
      :totalQuestionsNumber="this.questions.length"
    />

    <b-container>
      <b-row>
        <b-col sm="6" offset="3">
          <QuestionBox v-if="this.questions.length > 0"
            :currentQuestion="this.questions[index]"
            :next="this.next"
          />
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import QuestionBox from "./components/QuestionBox.vue";

export default {
  name: "app",
  components: {
    Header,
    QuestionBox
  },
  data() {
    return {
      questions: [],
      index: 0
    };
  },
  methods: {
    next() {
      this.index++
    }
  },
  mounted: function() {
    fetch('https://opentdb.com/api.php?amount=10&category=20&type=multiple', {
      method: 'get'
    })
      .then((response) => {
        return response.json()
      })
      .then((jsonData) => {
        this.questions = jsonData.results
      });
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

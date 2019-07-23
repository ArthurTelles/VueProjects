<template>
  <div>
    <b-nav tabs>
      <b-nav-item disabled><b>First Quiz App</b></b-nav-item>
      <b-nav-item disabled>
          Counter: {{this.currentQuestionNumber}}/{{totalQuestionsNumber}}
      </b-nav-item>
    </b-nav>
  </div>
</template>

<script>
export default {
    props: [
        'currentQuestionNumber',
        'totalQuestionsNumber'
    ]
}
</script>

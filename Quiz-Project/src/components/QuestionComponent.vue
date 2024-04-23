<template>
  <div class="questions-ctr">
    <div class="progress">
      <div class="bar" :style="{width: `${questionsAnswered / questions.length * 100}%`}"></div>
      <div class="status">{{ questionsAnswered }} out of {{ questions.length }} questions answered</div>
    </div>
    <transition-group name="fade">
      <div class="single-question" v-for="(question, index) in questions" :key="question.q"
           v-show="index === questionsAnswered">
        <div class="question">{{ question.q }}</div>
        <div class="answers">
          <div class="answer" v-for="answer in question.answers" :key="answer.text"
               @click.prevent="questionAnswered(answer.is_correct)">{{ answer.text }}
          </div>
        </div>
      </div>
    </transition-group>
  </div>
</template>

<script>
export default {
  name: "QuestionComponent",
  props: ["questions", "questionsAnswered"],
  emits: ["questionAnswered"],
  methods: {
    questionAnswered(is_correct) {
      this.$emit("questionAnswered", is_correct)
    }
  }
}
</script>
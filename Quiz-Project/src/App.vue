<template>
  <div class="ctr">
    <transition name="fade" mode="out-in">
      <QuestionComponent
          v-if="questionsAnswered < questions.length"
          :questions="questions"
          :questions-answered="questionsAnswered"
          @questionAnswered="questionAnswered"
      />
      <ResultComponent
          v-else
          :results="results"
          :total-correct="totalCorrect"
      />
    </transition>
    <button type="button" class="reset-btn" @click.prevent="reset" v-if="questionsAnswered === questions.length">Reset</button>
  </div>
</template>

<script>
import QuestionComponent from "@/components/QuestionComponent.vue";
import ResultComponent from "@/components/ResultComponent.vue";

export default {
  name: "App",
  components: {QuestionComponent, ResultComponent},
  methods: {
    questionAnswered(is_correct) {
      if (is_correct) {
        this.totalCorrect++;
      }
      this.questionsAnswered++;
    },
    reset() {
      this.totalCorrect = 0;
      this.questionsAnswered = 0;
    }
  },
  data() {
    return {
      totalCorrect: 0,
      questionsAnswered: 0,
      questions: [
        {
          q: 'What is 2 + 2?',
          answers: [
            {
              text: '4',
              is_correct: true
            },
            {
              text: '3',
              is_correct: false
            },
            {
              text: 'Fish',
              is_correct: false
            },
            {
              text: '5',
              is_correct: false
            }
          ]
        },
        {
          q: 'How many letters are in the word "Banana"?',
          answers: [
            {
              text: '5',
              is_correct: false
            },
            {
              text: '7',
              is_correct: false
            },
            {
              text: '6',
              is_correct: true
            },
            {
              text: '12',
              is_correct: false
            }
          ]
        },
        {
          q: 'Find the missing letter: C_ke',
          answers: [
            {
              text: 'e',
              is_correct: false
            },
            {
              text: 'a',
              is_correct: true
            },
            {
              text: 'i',
              is_correct: false
            }
          ]
        },
      ],
      results: [
        {
          min: 0,
          max: 2,
          title: "Try again!",
          desc: "Do a little more studying and you may succeed!"
        },
        {
          min: 3,
          max: 3,
          title: "Wow, you're a genius!",
          desc: "Studying has definitely paid off for you!"
        }
      ]
    }
  }
}
</script>

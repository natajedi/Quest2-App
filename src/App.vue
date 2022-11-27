<script setup>
import { ref, computed } from 'vue'

const questions = ref([
{ 
   question: 'qestion1?',
   answer: 0,
   options: [
   'answer',
   'answer',
   'answer '
 ],
 selected: null
},
{ 
   question: 'qestion2?',
   answer: 2,
   options: [
   '1answer',
   '2answer',
   '3answer'
 ],
 selected: null
},
{ 
   question: 'qestion3?',
   answer: 1,
   options: [
   '1answer',
   '2answer',
   '3answer'
 ],
 selected: null
}
])

const quizCompleted = ref(false)
const currentQuestion = ref(0)
const score = computed(() => {
  let value = 0
  questions.value.map(q => {
       if (q.selected == q.answer) {
          value++
      }
   })
   return value
})

const getCurrentQuestion = computed(( ) => {
  let question = questions.value[currentQuestion.value]
  question.index = currentQuestion.value
  return question
})

const SetAnswer = evt => {
    questions.value[currentQuestion.value].selected = evt.target.value
    evt.target.value = null
}

const NextQuestion = () => {
  if (currentQuestion.value < questions.value.length - 1) {
     currentQuestion.value++
  } else {
     quizCompleted.value = true
  }
}

</script>

<template>
  <main class="app">
<h1>The Quiz</h1>

<section class="quiz">
   <div class="quiz-info">
      <span class="question">{{ getCurrentQuestion.question }}</span>
      <span class="score">Score{{ score }}/{{ question.length }}</span>
   </div>
  </section>
</main>
</template>

<style>
*{
margin: 0;
padding: 0;
box-sizing: border-box;
font-family: 'Roboto', sans-serif;
}

body {
background-color: #125e51;
color: #FFF;
}
.app {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 2rem;
  min-height: 100vh;
}

h1 {
   font-size: 2rem;
   margin-bottom: 2rem;
   color: #FFF;
}
</style>

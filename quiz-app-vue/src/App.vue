<template>

      <div v-if="!quizStarted && !showResult">
        <h2 class="text-warning d-flex justify-content-center my-4 ">Quiz Guide</h2>
        <div class="container d-flex justify-content-center text-white w-50 flex-wrap">
            <h6 class="text-black">1. You have <cite class="text-yellow" style="color:yellow">05 seconds</cite> per each question</h6>
            <h6 class="text-black">2. once you select you answer it can't be undone</h6>
            <h6 class="text-black">3. you'il get pointed on the basic of your correct answers</h6>
            <h6 class="text-black">4. you can't Exit from the quiz while you are playing</h6>
        </div>
        <button @click="startQuiz" class="btn btn-outline-dark m-4">Start Quiz</button>
      </div>
      <div v-else-if="quizStarted">
        <h3 class="text-dark">{{ questions[currentQuestion].question }}</h3>
        <form @submit.prevent="submitAnswer" class="">
          <label class="w-100 text-start border bg-white m-2 p-2 rounded text-dark" v-for="(answer, index) in questions[currentQuestion].answers" :key="index">
            <input type="radio" :value="answer" v-model="selectedAnswer">
            {{ answer }}
          </label>
          <button type="submit" class="btn btn-outline-dark m-2">Submit Answer</button>
        </form>
        
      </div>
      <div v-else-if="showResult">
          <p>Score: {{ score }} / {{ questions.length }}</p>
          <button @click="restartQuiz" class="btn btn-outline-dark">Restart Quiz</button>
        </div>
   
</template>

<script>
export default {
  data(){
    return {
      quizStarted: false,
      questions: [
        {
          question: 'Qu est ce que c est que PHP?',
          answers: ['php est un langage de programmation qui permet de créer', 'php est un langage de programmation et lancé par Sun Microsystems en 1995.', 'php est un langage informatique permettant de mettre en forme des pages web', 'php est un langage de scripts généraliste et Open Source '],
          correctAnswer: 'php est un langage de scripts généraliste et Open Source '
        },
        {
          question: 'Qu elle est la dernière version stable de PHP?',
          answers: ['version 8.0.0', 'version 7.0.2', 'version 5.0.2', 'version 7.6.2'],
          correctAnswer: 'version 8.0.0'
        },
        {
          question: 'Quel type de langage PHP ? ',
          answers: ['script language', 'spécificateurs arithmétique', 'Statique', 'balisage'],
          correctAnswer: 'script language'
        },
        {
            question: 'AVG() ',
            answers: ['Returns the number of rows no', 'Returns the average value.', 'Returns the smallest value', 'Returns the number of rows'],
            correctAnswer: 'Returns the average value.'
          }
      ],
      currentQuestion: 0,
      selectedAnswer: null,
      score: 0,
      showResult: false
    }
  },
  methods:{
    startQuiz() {
        this.quizStarted = true;
      },
      submitAnswer() {
        if (this.selectedAnswer === this.questions[this.currentQuestion].correctAnswer) {
          this.score++;
        }
        this.currentQuestion++;

        this.selectedAnswer = null;
      
        if (this.currentQuestion == this.questions.length) {
          this.showResult = true;
          this.quizStarted = false;
        }
        
      },
      restartQuiz() {
        this.quizStarted = false;
        this.currentQuestion = 0;
        this.selectedAnswer = null;
        this.score = 0;
        this.showResult = false;
      }
  },

}
</script>

<style>
body {
    font-family: Arial, sans-serif;
    background: #fffefed1;
  }
  
  #app {
    max-width: 800px;
    margin: 0 auto;
    text-align: center;
  }
  
  h1 {
    margin-top: 0;
  }
  
  form {
    margin-top: 20px;
  }
  
  button {
    margin-top: 10px;
  }
  
  p {
    margin-top: 20px;
  }
  

</style>
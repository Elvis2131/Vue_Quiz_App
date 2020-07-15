<template>
    <div>
  <b-jumbotron>
    <template v-slot:lead>
      {{CurrentQuestion.question}}<br>
       <b-badge variant="warning">Question difficulty: {{CurrentQuestion.difficulty}}</b-badge>
    </template>

    <hr class="my-4">

    <!-- <p v-for=" (answers,index) in answers" :key="index">
          {{answers}}
    </p> -->
    <b-list-group>
        <b-list-group-item button v-for=" (answers,index) in answers" :key="index" @click="selectAnswer(index)"
        :class="[
        !answered && selectedIndex === index ? 'selected' : 
        answered && correctIndex === index ? 'correct' : 
        answered && correctIndex !== index ? 'incorrect': ''
        ]">{{answers}}</b-list-group-item>
    </b-list-group>

    <b-button 
    variant="primary" 
    @click="submitAnswer"
    :disabled="selectedIndex === null || answered">Submit</b-button>
    <b-button @click = "next" variant="success" href="#">Next</b-button>
  </b-jumbotron>
</div>
</template>

<script>
import _ from 'lodash'

export default {
    props:{
        CurrentQuestion: Object,
        next: Function,
        increment: Function
    },
    data(){
        return{
            selectedIndex: null,
            correctIndex: null,
            shuffledAnswers: [],
            answered: false
        }
    },
    computed:{
        answers(){
            let answers = [...this.CurrentQuestion.incorrect_answers]
            answers.push(this.CurrentQuestion.correct_answer)
            return answers
        }
    },
    watch:{
        CurrentQuestion:{
            immediate: true,
            handler(){
                this.selectedIndex = null
                this.shuffleAnswers()
                this.answered = false
            }
        }
    },
    methods:{
        selectAnswer(index){
            this.selectedIndex = index
        },
        shuffleAnswers(){
           let answers = [...this.CurrentQuestion.incorrect_answers, this.CurrentQuestion.correct_answer]
           this.shuffledAnswers = _.shuffle(answers)
           this.correctIndex = this.shuffledAnswers.indexOf(this.CurrentQuestion.correct_answer)
        },
        submitAnswer(){
            let isCorrect = false

            if(this.selectedIndex === this.correctIndex) {
                isCorrect = true
            }
            this.answered === true
            this.increment(isCorrect)
        }
    },
}
</script>

<style scoped>
.list-group{
    margin-bottom: 15px;
}
.btn{
    margin: 0 5px;
}

.selected{
    background-color: #FE8A2D;
    color: white;
}

.correct{
    background-color: #00A26B;
    color: white;
}

.incorrect{
    background-color: #EC005F;
    color: white;
}
</style>
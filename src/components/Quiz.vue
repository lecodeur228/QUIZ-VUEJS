<template>

    <div >

        <h1>{{ quiz.title }}</h1>
        <Progress :value="step " :max="quiz.questions.length " />

        <Question :question="question" v-if="state === 'question'" @answer="addAnswer" />

        <Recap v-if="state === 'recap'" :quiz="quiz" :answers="answers" />

        {{ answers }}
    </div>

</template>

<script setup>

import { computed, ref } from 'vue';
import Progress from './progress.vue';
import Question from './Question.vue';
import Recap from './Recap.vue';

const step = ref(0);
const state =  ref('question');

   const props = defineProps({
        quiz: Object
    });

    const question =  computed(() => props.quiz.questions[step.value]);

    const answers =  ref(props.quiz.questions.map(() => null));

    const addAnswer =  (answer) => {
        answers.value[step.value] = answer;
       if ( step.value === props.quiz.questions.length -1 ) {
           state.value  =  'recap';
       } else {
           step.value ++;
        
       }
    }
</script>

<style>
.question {
    padding-top: 2rem;
}
</style>

<template>

    <div class="question">
        <h3> {{ question.question }} </h3>
     
            <ul>
                <li v-for="(choise,index) in randonChoises" :key="choise" >
                    <Answer :id="`answer${index}`" :value="choise" v-model="answer" :disabled="hasAnswer" :correctAnswer="question.correct_answer" />
                 
                </li>
            </ul>
          
            <button :disabled="!hasAnswer" @click="emits('answer', answer)">Question suivante</button>

    </div>
</template>

<script setup>
import { computed, ref, watch } from 'vue';
import { shuffleArray } from './functions/array';
import Answer from './Answer.vue';


const props = defineProps({
    question: Object,
})

const answer = ref(null);
const emits = defineEmits(['answer']);
const hasAnswer = computed(() => answer.value !== null);

watch(() => props.question, () => {
    answer.value = null;

});

const randonChoises = computed(() => shuffleArray(props.question.choices));

</script>

<style>
.question button{
    margin-left: auto;
    display: block;
}
</style>
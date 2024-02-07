
<script setup>
import { defineProps } from 'vue';
import questions from '~/data/questions';

// Saves the current step of the survey as a reference, defaults to 0
const currentStep = ref(0);
const answers = ref([]);
const selectedAnswer = ref('');
const errorMessage = ref('');

// Increments the current step by 1, if the current step is less than the total number of questions, otherwise navigates to the results page
const incrementStep = () => {
    if (selectedAnswer.value === '') {
        errorMessage.value = 'Please select an answer';
        return;
    }

    answers.value.push(selectedAnswer.value);
    currentStep.value++;
    selectedAnswer.value = '';
    errorMessage.value = '';

    // If the current step is greater than or equal to the total number of questions, end the quiz
    if (currentStep.value >= questions.length) {
        return;
    }
}

</script>

<template>
    <div v-if="currentStep < questions.length">
        <h1>Welcome to the state survey!</h1>

        <article>
            <h2>Question {{ questions[currentStep].id }}</h2>
            <form>
                <p>{{ questions[currentStep].question }}</p>
                <div v-for="answer in questions[currentStep].answers">
                    <input type="radio" :id="answer.toLowerCase()" :value="answer.toLowerCase()" v-model="selectedAnswer" />
                    <label :for="answer.toLowerCase()">{{ answer }}</label>
                </div>
            </form>
        </article>
        <p v-if="errorMessage">{{ errorMessage }}</p>
        <button @click="incrementStep">Next question</button>
    </div>
    <div v-else>
        <h2>Thank you for completing the survey!</h2>
        <h3>Here are your answers:</h3>
        <p v-for="answer in answers">{{ answer }}</p>
    </div>
</template>


<script setup>
import { defineProps } from 'vue';
import questions from '~/data/questions';

// Saves the current step of the survey as a reference, defaults to 0
const currentStep = ref(0);
const answers = ref([]);
const selectedAnswer = ref('');
const errorMessage = ref('');

watch(selectedAnswer, () => {
    errorMessage.value = '';
});

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

const restartQuiz = () => {
    currentStep.value = 0;
    answers.value = [];
}

</script>

<template>
    <section v-if="currentStep < questions.length">
        <article>
            <h2>Question {{ questions[currentStep].id }}</h2>
            <form>
                <p>{{ questions[currentStep].question }}</p>
                <div class="radio-buttons" v-for="answer in questions[currentStep].answers">
                    <input type="radio" :id="answer.toLowerCase()" :value="answer.toLowerCase()" v-model="selectedAnswer" />
                    <label :for="answer.toLowerCase()">{{ answer }}</label>
                </div>
            </form>
        </article>
        <p class="error" v-if="errorMessage">{{ errorMessage }}</p>
        <button @click="incrementStep">Next question</button>
    </section>
    <section v-else>
        <h3>Here is your current state</h3>
        <p>It is {{ answers[0] }} outside, and your in a {{ answers[1] }} mood. That may be because you are {{ answers[2]
        }}.
        </p>
        <button @click="restartQuiz">Restart</button>
    </section>
</template>

<style lang="scss" scoped>
section {
    padding: 1rem;

    .radio-buttons {
        display: flex;
        gap: 0.5rem;
        align-items: center;
        justify-content: center;

        input[type="radio"] {
            margin: 0;
        }

        p {
            line-height: 0;
        }
    }

    button {
        padding: 0.6rem 1rem;
        border-radius: 20px;
        border: none;
        background: #7F27FF;
        color: white;
        font-size: 14px;

        &:hover {
            background: #9F70FD;
            text-decoration: underline;
            transform: scale(1.05);
            transition: all 0.3s ease-in-out;
        }
    }

    .error {
        color: red;
    }
}
</style>
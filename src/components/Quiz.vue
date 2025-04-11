<template>
    <div class="container">
       <h1> {{ quiz.title }}</h1>
       <Progress :value="step" :max="quiz.questions.length - 1" />
       <Questions :question="q" v-if="q" @answer="addAnswer"/>
       {{ answers }}
    </div>
</template>

<script setup>
    import { computed, ref } from 'vue';
    import Progress from './Progress.vue';
    import Questions from './Questions.vue';


   const props = defineProps({
        quiz : Object
    })

    const answers = ref(props.quiz.questions.map(()=> null))
    const step = ref(0)
    const q = computed(() => props.quiz.questions[step.value])
    const addAnswer = (answer) => {
        answers.value[step.value] = answer
    }
</script> 

<style>
    .container {
        width: 600px;
        margin : 0 auto
    }
</style>
<template>
    <div v-if="state === 'error'">
        Impossible de charger le Quiz
    </div>
    <div v-else>
        <Quiz :quiz="quiz" v-if="quiz"/>
    </div>
</template>

<script setup>
import {onMounted, ref} from "vue"
import Quiz from "./components/Quiz.vue"

    const quiz = ref(null)
    const state = ref('loading')
    
    onMounted(() => {
      fetch('./quiz.json')
          .then(r => {
               if(r.ok) {
                 return r.json()
               }
               throw new Error('Impossible de contacter le serveur!')
          })
          .then(data => {
            quiz.value = data
            state.value = 'idle'
          })
          .catch((e) => {
            state.value = 'error'
          })
    })


</script>
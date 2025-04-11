<template>
  <div v-if="state === 'error'">
      Il y a une erreur qui se produit
  </div>
  <div v-else>
    {{ quiz }}
  </div>
</template>

<script setup>
import {onMounted, ref} from "vue"

    const quiz = ref(null)
    const state = ref('loading')
    
    onMounted(() => {
      fetch('./quizs.json')
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
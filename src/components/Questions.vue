<template>
    <div class="question">
        <h3>{{ question.question }}</h3>
    </div>
    <ul>
        <li v-for="(choice,index) in question.choices" :key="choice">
            <label :for="index">
                <input :id="index" type="radio" name="answer" v-model="answer" :value="choice">
                {{ choice }}
            </label>
        </li>
       
        
    </ul>
    <button :disabled="!hasAnswer" @click="emits('answer', answer)">Questions suivantes</button>

</template>

<script setup>
    import {computed, ref, watch} from "vue"

    const answer = ref(null)
    const emits = defineEmits(['answer'])

    const props = defineProps({
        question : Object
    })

    const hasAnswer = computed(() => answer.value !== null)

   
</script>


<style>
    .question h3{
        padding-top: 15px;
    }
    
</style>
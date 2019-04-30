<template>
    <div class="api">
        <AllQuestion v-bind:questions="questions"/>
        <AddQuestion v-on:add-question="addQuestion" />
    </div>
</template>
<script>
import AllQuestion from './AllQuestion';
import AddQuestion from './AddQuestion';
export default {
    name: 'Api',
    data(){
        return {
            questions:[],
            allQ:false
            }  
    },
    created: function()
        {
            this.allQuestions();
        },
    components :{
        AllQuestion,
        AddQuestion
    },
    methods: {
        allQuestions: async function(){
            let question = await fetch(`http://localhost:3000/questions`, { method: 'get', headers: { 'Content-Type': 'application/json'}})
            let data = await question.json();
            this.questions=data;
            
        },
       async addQuestion(newQuestion){
            let question = await fetch(`http://localhost:3000/questions`, { method: 'post', headers: { 'Content-Type': 'application/json'}, body: JSON.stringify({ 'id': newQuestion.id, 'question_text': newQuestion.question_text, 'option_1': newQuestion.option_1,'option_2': newQuestion.option_2,'option_3': newQuestion.option_3, 'option_4': newQuestion.option_4, 'answer': newQuestion.answer })})
            let data = await question.json();
            this.questions=[...this.questions , data];
        }
    }
}
</script>
<style scoped>
.api{
    margin: 2em 0 0 10%;
    display: flex;
    justify-content: space-around;
}
</style>
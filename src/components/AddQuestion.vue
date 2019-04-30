<template>
    <div class="add-container">
      <h1 class="title">Add Questions</h1>
      <form @submit="addQuestion">
        <label>Question</label>
        <br>
         <textarea v-model="question" name="textarea" placeholder="add new question" />
         <br>
         <label>Option 1</label>
         <br>
         <input v-model="option1" type="text">
         <br>
         <label>Option 2</label>
         <br>
         <input v-model="option2" type="text">
         <br>
         <label>Option 3</label>
         <br>
         <input v-model="option3" type="text">
         <br>
         <label>Option 4</label>
         <br>
         <input v-model="option4" type="text">
         <br>
         <label>Answer</label>
         <br>
         <input v-model="answer" type="text">
         <br>
         <button type="submit">Add</button>
      </form>
    </div>
</template>
<script>
import uuid from 'uuid';
export default {
    name:'AddQuestion',
    props: {questions :Array},
    data(){
        return{
            question:'',
            option1:'',
            option2:'',
            option3:'',
            option4:'',
            answer:'',
        }
    },
    methods: {
        addQuestion(e){
            e.preventDefault();
            const newQuestion={
                id: uuid.v4(),
                question_text: this.question,
                option_1: this.option1,
                option_2: this.option2,
                option_3: this.option3,
                option_4: this.option4,
                answer: this.answer,
                completed:false
            }
            this.$emit('add-question', newQuestion);
            this.question='';
            this.option1='';
            this.option2='';
            this.option3='';
            this.option4='';
            this.answer='';
        }
    }
}
</script>
<style scoped>
.add-container{
    border: 1px solid cadetblue;
    padding: 1em;
    height: 550px;
}
.title{
    border-bottom:1px solid darkgray; 
}
textarea{
    padding: 1em;
}
input{
    margin: 1em 0;
}
button{
    margin-left: 30%;
}
</style>
<template>
    <div class="all-question">
            <h1>All Questions</h1>
            <hr>
            <div class="show-container" v-for="question in questions" :key="question.id">
                <div v-if="!isEditing" :id="question.id">
                    <p><strong>Q.{{question.question_text}}</strong></p>
                    <p>A. {{question.option_1}}</p>
                    <p>B. {{question.option_2}}</p>
                    <p>C. {{question.option_3}}</p>
                    <p>D. {{question.option_4}}</p>
                    <p>Answer:{{question.answer}}</p>
                </div>
                <div class="edit-container">
                    <button @click.prevent="populateQuestionToEdit(question)" v-if="!isEditing" :id="question.id" >Edit</button>
                </div>
            </div>
            <div v-if="isEditing">
                <form>
                    <label>Question</label>
                    <br>
                    <textarea v-model="model.question_text" name="textarea" placeholder="add new question" :class="{view: !isEditing}" />
                    <br>
                    <label>Option 1</label>
                    <br>
                    <input v-model="model.option_1" type="text" :class="{view: !isEditing}">
                    <br>
                    <label>Option 2</label>
                    <br>
                    <input v-model="model.option_2" type="text" :class="{view: !isEditing}">
                    <br>
                    <label>Option 3</label>
                    <br>
                    <input v-model="model.option_3" type="text" :class="{view: !isEditing}">
                    <br>
                    <label>Option 4</label>
                    <br>
                    <input v-model="model.option_4" type="text" :class="{view: !isEditing}">
                    <br>
                    <label>Answer</label>
                    <br>
                    <input v-model="model.answer" type="text" :class="{view: !isEditing}">
                    <br>
                    <button type="submit" @click="save" v-if="isEditing">Save</button>
                    <button v-if="isEditing" @click="cancel">Cancel</button>
                </form>
            </div>
    </div>
</template>
<script>
export default {
    name:'AllQuestion',
    props: {questions :Array},
    data(){
        return{
            isEditing: false,
            model:{}
        }
    },
    async created () {
    this.refreshQuestions()
  },
    methods: {
        async populateQuestionToEdit (question) {
        this.model = Object.assign({}, question)
        this.isEditing=!this.isEditing;
    },
    async save(){
        let question = await fetch(`http://localhost:3000/questions/${this.model.id}`, { method: 'put', headers: { 'Content-Type': 'application/json'}, body: JSON.stringify({ 'question_text': this.model.question_text, 'option_1': this.model.option_1,'option_2': this.model.option_2,'option_3': this.model.option_3, 'option_4': this.model.option_4, 'answer': this.model.answer })})
        let data = await question.json();
        await this.refreshQuestions();
        this.isEditing = false;
        this.model={};
    },
    async refreshQuestions(){
            let question = await fetch(`http://localhost:3000/questions`, { method: 'get', headers: { 'Content-Type': 'application/json'}})
            let data = await question.json();
            this.questions=data;
        },
    cancel() {
      this.model= Object.assign({}, this.model);
      this.isEditing = false;
    }
    }
}
</script>
<style scoped>
    .all-question {
        width: 820px;
        display: inline-block;
        background: azure;
        padding-left: 1em;
    }
    .show-container{
        display: flex;
        
    }
    .edit-container{
        margin: .8em 0 0 1em;
    }
    .view {
  border-color: transparent;
  background-color: initial;
  color: initial
}
</style>


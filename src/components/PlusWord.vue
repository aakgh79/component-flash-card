<template>
  <div id ="tet">
    <h1>Add Word</h1>  
  <div class="modal">
  <input type="text" v-model="newWord.Word_A"  placeholder="word">
  <input type="text" v-model="newWord.Word_B" placeholder="answer">
  <input type="text" v-model="newWord.Hint" placeholder="hint">
  <button @click="addWord()" >add word</button>
  </div>
  </div>
  
  </template>
  
  <script>
  export default {
    emits: ['add-word'],
    data(){
        return{
          newWord:{
            Word_A:'',
            word_B:'',
            Hint:'',
          }
        }
    },
  
  methods:{
    addWord() {
   const newWord = {
    word_A: this.newWord.Word_A,
    word_B: this.newWord.Word_B,
    Hint: this.newWord.Hint,
  };
  this.$emit('add-word', newWord);
  this.newWord.Word_A = '';
  this.newWord.Word_B = '';
  this.newWord.Hint = '';
}
  }
  
  };
  </script>
  <style scoped>
  .modal {
display: flex;
flex-direction: column;
margin: 20px auto; 
width: 300px;
border-radius: 5px;
padding: 10px;
background-color: #E8F0FF;
  }
  button{
    background-color: green; color: yellow;
  }

  #let{
    margin-top: 2em;
  }

</style>
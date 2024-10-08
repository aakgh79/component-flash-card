<template>
  <h2>Flash Word</h2>

  <p v-if="completed" id="completed">Great, you completed all words!!</p>
  <p v-else="correctCount!=null" id="correctCount">you have answered {{ correctCount }} out of {{ WordCount }}</p>
  <p v-if="incorrectCount != null" id="correctCount">you have answered wrong{{ incorrectCount }} out of {{ WordCount }}
  </p>

  <div id="cards">
    <WordCard 
        v-for="(word ) in ShuffledWords"
        v-bind:word="word" @incrementCorrectCount="incrementCorrectCount();"
       @incrementInCorrectCount="incrementIncorrectCount();">
    </WordCard>

  </div>

  <div>
    <button @click="resetBtn()">reset all</button>
    <button @click="resetWrongAnswer()">reset wrong answer</button>
  </div>

<PlusWord @add-word="addWordToEnglishWords"  ></PlusWord>
  
</template>



<script>
import PlusWord from './components/PlusWord.vue';
import WordCard from './components/WordCard.vue'
export default {
  components:{WordCard,PlusWord},

  data() {
    return {
      EnglishWords: [
        {
          word_A: 'hola',
          word_B: 'hello',
          Hint: 'whats`s app',
          Answer: '',
          correct: false
        },
        {
          word_A: 'uno',
          word_B: 'one',
          Hint: 'number',
          Answer: '',
          correct: false
        },
        
        
      ],
      correctCount: null,
      incorrectCount: null,
      completed: false
      
    };
    
  },
  
  computed: {
    ShuffledWords() {
      return this.EnglishWords.sort(() => .5 - Math.random());
    },
    WordCount() {
      return this.EnglishWords.length;
    }
  },
  
  // this methods watching correctCount in methoud checkanswer order to if it equal versus the WordCount say alert congrats
  watch: {
    // correctCount() {
    //     if (this.correctCount == this.WordCount) {
      //         alert('congrats');
      //     }
      // },
      
      // Watcher for correctCount.
      // If correctCount equals WordCount, sets completed flag to true.
      correctCount() {
        this.completed = this.correctCount == this.WordCount;
      },
      incorrectCount() {
        if (this.incorrectCount >= 10) {
          this.resetBtn();
          alert('please be more careful and strive to answer correctly')
        }
        this.EnglishWords.forEach((word) => {
          if (this.incorrectCount >= 2) {
            word.Answer = '';
          }
        });
      },
    },



      methods: {
        addWordToEnglishWords(newWord) {
          this.EnglishWords.push(newWord)
        },

        incrementCorrectCount(){
          this.correctCount++;
        },
        
        incrementIncorrectCount(){
          this.incorrectCount++;
        },
        
        resetBtn() {
          if (this.ShuffledWords) {
            this.ShuffledWords.forEach((word) => {
              word.Answer = '';
              word.correct = false;
              word.incorrect = false;
            });
          }
          this.completed = false;
          this.correctCount = null;
          this.incorrectCount = null;
        },
        resetWrongAnswer() {
          this.ShuffledWords.forEach((word) => {
            if (word.incorrect) {
              word.Answer = '';
              word.incorrect = false;
            }
          });
        },
        
      }
    };
</script>


<style>
[v-cloak] {
  display: none;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: black;
  margin-top: 60px;
}

#cards {
  justify-content: center;
  display: grid;
  grid-template-columns: 350px 350px 350px;
  grid-gap: 30px;
}

button {
  margin: 15px;
  margin-top: 3em;
  padding: 10px;
  color: blue;
  background-color: #E8F0FF;
  border: 0;
  font-size: 20px;
  border-radius: 5px;
}

.card {
  background-color: #E8F0FF;
  border-radius: 5px;
  padding: 10px 0;
  font-size: 25px;
}

input[type=text] {
  border: 0;
  font-size: 25px;
  border-radius: 5px;
  margin-top: 5px;
  text-align: center;
  padding: 5px;
}

.word {
  font-weight: bold;
  padding: 0;
  margin: 0;
}

.correctanswer {
  padding: 0;
  margin: 0;
}

.correct {
  color: #0f5132;
  background-color: #d1e7dd;
}

.incorrect {
  color: #db4343;
  background-color: #E8F0FF;
}

#correctCount {
  font-size: 20px;
  margin: 10px;
  font-weight: bold;
  padding: 10px;
}

#completed {
  font-size: 20px;
  font-weight: bold;
  color: #0f5132;
  padding: 10px;
  margin: 10px;
}

</style>
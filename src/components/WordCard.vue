<template lang="">
<div class='card'  v-bind:class='{ correct: word.correct, incorrect:word.incorrect }'>
      <p class="word">{{ word.word_A }}</p>
      <input type="text" v-if="!word.correct" v-model="word.Answer" @keyup.enter="CheckAnswer()">
      <p v-else class="correct.word_B">{{ word.word_B }}</p>
      <p v-if="word.incorrect >= 3">{{ word.Hint }}</p>
    </div>
    <!-- <div v-for="(word, index) in words" :key="index"></div> -->
</template>
<script>
export default {
    name: 'WordCard',
    props: {word: Array},
    data() {
        return {

        }
    },

    methods: {

        reset() {
      this.word.Answer = '';
      this.word.correct = false;
      this.word.incorrect = false;
    },


        CheckAnswer() {
            this.word.correct = this.word.word_B == this.word.Answer;
            this.word.incorrect = this.word.word_B !== this.word.Answer;
            if (this.word.correct) {
                this.$emit('incrementCorrectCount');
            } else {
                this.$emit('incrementInCorrectCount');
            }
            console.log(this.word.correct);
            debugger;
            console.log(this.word.incorrect);
        },
        
    }
};
</script>
<style scoped>
.card {
    background-color: #E8F0FF;
    border-radius: 5px;
    padding: 10px 0px;
    font-size: 25px;
}

input[type=text] {
    border: 0;
    font-size: 22px;
    border-radius: 5px;
    margin-top: 5px;
    text-align: center;
    padding: 5px;
}

.word {
    font-weight: bold;
}

.correctAnswer {
    padding: 0;
    margin: 0;
}

.correct {
    color: #0f5132;
    background-color: #d1e7dd;
}
</style>
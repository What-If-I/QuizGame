<template>
<div class="card">
  <transition name="swap" appear mode="out-in">
  <div class="question" v-if="!showAnswer" key="question">
    <p>{{question}}</p>
    <ul>
        <li v-for="answer in answers" :key="answer.id"><button @click="submitAnswer(answer)">{{answer}}</button></li>
    </ul>
  </div>

  <div class="result" v-else key="answer">
    <p>{{result}}</p>
    <button @click="resetGame">Давай ещё раз</button>
  </div>
  </transition>
</div>
</template>

<script>
export default {
  data() {
    return {
      qValues: [this.genRandomNumber(), this.genRandomNumber()],
      result: "",
      showAnswer: false
    };
  },
  methods: {
    submitAnswer(answer) {
      this.result =
        answer == this.correctAnswer ? "Правильно!" : "Не угадал(а)";
      this.showAnswer = true;
    },
    genRandomNumber(max = 100) {
      let random = Math.round(Math.random() * max);
      if (random === 0) {
        return 1;
      } else {
        return random;
      }
    },
    resetGame() {
      this.qValues = [this.genRandomNumber(), this.genRandomNumber()];
      this.result = "";
      this.showAnswer = false;
    }
  },
  computed: {
    question() {
      return `${this.qValues[0]} + ${this.qValues[1]} = ?`;
    },
    correctAnswer() {
      return this.qValues.reduce((a, b) => a + b);
    },
    answers() {
      let answers = [
        this.correctAnswer + this.genRandomNumber(15),
        this.correctAnswer - this.genRandomNumber(10),
        this.correctAnswer + this.genRandomNumber(5)
      ];
      answers.splice(this.genRandomNumber(3), 0, this.correctAnswer);
      return answers;
    }
  }
};
</script>

<style scoped>
p {
  font-size: 1.3rem;
  font-weight: 600;
}
.card {
  width: 300px;
  height: 250px;
  display: flex;
  text-align: center;
  justify-content: center;
  align-items: center;
  box-shadow: inset 0 0 10px 0px rgba(0, 0, 0, 0.5);
  padding: 10px 100px;
  background-color: rgb(215, 235, 253);
}
ul {
  display: flex;
  width: 100%;
  justify-content: space-between;
  flex-wrap: wrap;
  padding: 0 0 10px 0;
}
li {
  list-style: none;
  width: 45%;
  padding-top: 15px;
}
button {
  width: 100%;
  font-size: 1.3rem;
  font-weight: 100;
  display: block;
  border: none;
  background-color: cornflowerblue;
  padding: 14px 28px;
  box-shadow: 0 0 5px;
  transition: background-color 0.1s linear;
  cursor: pointer;
}
button:hover {
  background-color: aqua;
}
.green {
  background-color: green;
}
.swap-enter {
  transform: rotateY(90deg);
}
.swap-enter-to {
  transform: rotateY(0deg);
  transition: transform 0.2s linear;
}
.swap-leave {
  transform: rotateY(0deg);
}
.swap-leave-to {
  transform: rotateY(90deg);
  transition: transform 0.2s linear;
}
</style>

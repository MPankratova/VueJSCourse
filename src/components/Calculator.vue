<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <h3>Calculator</h3>
    <h3>X</h3><input type="text" v-model.number="numberOne"> {{ numberOne }}
    <h3>Y</h3><input type="text" v-model.number="numberTwo"> {{ numberTwo }}
    <h3>Результат: {{ result }}</h3>
    <h3>Результат при использовании последовательности Фибоначчи: {{ resultFib }}</h3>
    
    <button v-for="op in operations" 
      :key="op" 
      :disabled="numberOne === '' || numberTwo === ''"
      @click="calc(op)">
      {{ op }}
    </button>

    <div>
      <input type="checkbox" name="checkbox" id="checkbox" class="checkbox" v-model="checked">
      <label for="checkbox">Включить экранную клавиатуру</label>
      <div class="onScreen" v-if="checked">
        <h2>Экранная клавиатура</h2>
        <button v-for="num in screeOnKeyboard"
        :key="num"
        @click="addNumber(num)">
          {{ num }}
        </button>
        <div class="radio">
          <input type="radio"  id="radio1" value="X" v-model="picked">
          <label for="radio1"> X </label>
          <input type="radio"  id="radio2" value="Y" v-model="picked">
          <label for="radio1"> Y </label>
        </div>
      </div>
    </div>


    <div class="error" v-if="error">
      {{ error }}
    </div>

    <div class="result" v-if="result < 0">
      Получилось отрицательное число
    </div>

    <div class="result" v-else-if="result == 0">
      Вычислений нет
    </div>

    <div class="result" v-else-if="0 < result <= 1000">
      Результат лежит в пределах [1, 1000]
    </div>

    <div class="result" v-else-if="1000 < result <= 100000">
      Результат лежит в пределах [1000, 100000]
    </div>

    <div class="result" v-else>
      Результат слишком большой
    </div>

    <div class="logs">
      <div v-for="(log, id) in logs" :key="id"> {{ id }} - {{ log }} </div>
    </div>


  </div>
</template>

<script>
import Vue from 'vue';
export default {
  name: 'Calculator',
  props: {
    msg: String
  },
  data() {
    return {
      numberOne: '',
      numberTwo: '',
      result: '',
      resultFib: '',
      operations: ['sub', 'add', 'mult', 'div', 'exp', 'divInt'],
      error: '',
      logs: {},
      checked: false,
      screeOnKeyboard: ['0', '1', '2', '3', '4', '5', '6', '7', '8', '9', '<-'],
      picked: ''
    }
  },
  methods: {
    calc(op) {
      const  { numberOne, numberTwo } = this;
      this.error = '';
      Vue.set(this.logs, Date.now(), `${numberOne}${op}${numberTwo}=${this.result}`);
      switch(op) {
        case 'sub':
          this.result = numberOne - numberTwo;
          break;
        case 'add':
          this.result = numberOne + numberTwo;
          break;
        case 'mult':
          this.result = numberOne * numberTwo;
          break;
        case 'div':
          if (numberTwo == 0) {
            this.error = 'Делить на 0 нельзя'
          } else {
            this.result = numberOne / numberTwo;
          }          
          break;  
        case 'exp':
          this.result = Math.pow(numberOne, numberTwo);
          break;  
        case 'divInt':
          if (numberTwo == 0) {
            this.error = 'Делить на 0 нельзя'
          } else {
            this.result = Math.round(numberOne / numberTwo);
          }
          break;          
      }
    },
    
    addNumber(num) {
      if (num == '<-') {
        if (this.picked == 'X') {
          let strNumberOne = String(this.numberOne);
          return this.numberOne = +(strNumberOne.substr(0, strNumberOne.length - 1));
        } else if (this.picked == 'Y') {
          let strNumberTwo = String(this.numberTwo);
          return this.numberTwo = +(strNumberTwo.substr(0, strNumberTwo.length - 1));
        }
      } else {
        if (this.picked == 'X') {
          return this.numberOne = +(String(this.numberOne) + num);
        } else if (this.picked == 'Y') {
          return this.numberTwo = +(String(this.numberTwo) + num);
        }
      }
    }
  },
  computed: {

  }

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.error {
  padding: 20px;
  margin: 20px 0 0;
  border: 1px solid red ;
}

.result {
  padding: 20px;
  margin: 20px 0 0;
  border: 1px solid green ;
}

.onScreen {
  padding: 10px;
  margin: 20px 0 0;
  border: 3px solid blue ;
  color: blue;
}

.checkbox {
  padding: 10px;
  margin: 20px 0 0;
}

.radio {
  padding: 10px;
  margin: 20px 0 0;
  border: 3px solid black ;
}
</style>

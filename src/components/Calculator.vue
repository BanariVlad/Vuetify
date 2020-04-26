<template>
  <div class="d-flex" style="height: 100vh">
    <v-container 
      class="align-self-center" 
      style="width: 350px"
    >
      <v-row>
        <v-btn 
          dark depressed 
          class="cyan clear" 
          @click="clear()"
        >
          Clear
        </v-btn>
        <p class="subheading text-right">20 + 107</p>
        <p class="display-1 text-right">127</p>
      </v-row>
      <v-row class="cyan white--text">
        <v-col 
          v-for="operation in operations" 
          :key="operation"
          class="text-center"
        >
          <button 
            class="button"
            @click="updateCurrentNumber(operation)"
          >
            {{operation}}
          </button>
        </v-col>
      </v-row>
      <v-row 
        wrap 
        class="grey darken-3 white--text"
      >
        <v-col
          cols="4" 
          v-for="number in numbers" 
          :key="number" 
          style="height: 75px"
          class="text-center"
        >
         <button
            :class='number === numbers[numbers.length - 1] ? "equal" : "button"'
            @click="addDigit(number)"
          >
            {{number}}
          </button>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<script>
export default {
  data() {
    return {
      numbers: [1, 2, 3, 4, 5, 6, 7, 8, 9, '.', 0, '='],
      operations: ['/', '*', '-', '+'],
      currentOperation: '',
      currentNumber: '',
      prevNumber: ''
    };
  },
  methods: {
    addDigit(newNumber) {
      let currentNumberOut = document.querySelector('p.display-1');
      let prevNumberOut = document.querySelector('p.subheading');
      if (newNumber !== '=' && this.currentNumber.length < 12) {
        if (newNumber === '.' && this.currentNumber.includes('.')) {
          return;
        }
        if (newNumber === '.' && this.currentNumber.length === 0) {
          this.currentNumber = '0';
        }
        this.currentNumber += newNumber;
        currentNumberOut.innerText = this.currentNumber;
      } else if (newNumber === '=') {
        this.updateCurrentNumber(this.currentOperation);
        prevNumberOut.innerText = '';
        currentNumberOut.innerText = this.prevNumber;
      }
    },

    updateCurrentNumber(operation) {
      let currentNumberOut = document.querySelector('p.display-1');
      let prevNumberOut = document.querySelector('p.subheading');
      if (!this.currentOperation) {
        prevNumberOut.innerText = this.currentNumber;
        currentNumberOut.innerText = '';
        this.prevNumber = this.currentNumber;
        this.currentNumber = '';
        this.currentOperation = operation;
        return;
      }
      switch(this.currentOperation) {
        case '+':
          this.prevNumber = Number(this.prevNumber) + Number(this.currentNumber);
        break;
        case '-':
          this.prevNumber = Number(this.prevNumber) - Number(this.currentNumber);
        break;
        case '*':
          this.prevNumber = Number(this.prevNumber) * Number(this.currentNumber);
        break;
        case '/':
          if (this.currentNumber === '0') {
            this.prevNumber = 'Error';
          } else {
            this.prevNumber = Number(this.prevNumber) / Number(this.currentNumber);
          }
        break;
      }
      prevNumberOut.innerText = this.prevNumber;
      currentNumberOut.innerText = '';
      this.currentNumber = '';
      this.currentOperation = operation;
    }, 

    clear() {
      document.querySelector('p.display-1').innerText = '';
      document.querySelector('p.subheading').innerText = '';
      this.currentNumber = '';
      this.prevNumber = '';
      this.currentOperation = '';
    }
  }
};
</script>

<style scoped>
  .button, .equal {
    width: 50px;
    height: 50px;
    border-radius: 50%;
    cursor: pointer;
    outline: none;
    transition: .2s;
    font-size: 25px;
  }

  .button:hover {
    background-color: #23262E;
    color: #fff;
  }

  p {
    background-color: #fff;
    display: block;
    width: 100%;
    margin: 0 !important;
    height: 60px;
    padding: 0 10px;
  }

  p.subheading {
    padding-top: 30px;
  }

  .clear {
    top: 36px;
    border-radius: 0;
  }
  .equal {
    background-color: orange;
  }
</style>
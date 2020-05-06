<template>
  <div class="d-flex" style="height: 100vh">
    <v-container class="align-self-center" style="width: 300px">
      <v-row>
        <v-btn small dark depressed fab class="clear cyan" @click="clear()">C</v-btn>
        <p class="white caption">{{prevNumber}}</p>
        <p class="white display-1">{{currentNumber}}</p>
      </v-row>
      <v-row class="cyan white--text">
        <v-col v-for="operation in operations" :key="operation" class="text-center">
          <v-btn
            fab
            depressed
            dark
            small
            color="cyan"
            style="font-size: 25px"
            @click="changeOperation(operation)"
          >{{operation}}</v-btn>
        </v-col>
      </v-row>
      <v-row wrap class="grey darken-3 white--text">
        <v-col
          cols="4"
          v-for="number in numbers"
          :key="number"
          style="height: 75px"
          class="text-center"
        >
          <v-btn
            fab
            text
            :color="number === '=' ? 'orange' : ''"
            class="white--text"
            style="font-size: 25px"
            @click="addNumber(number)"
          >{{number}}</v-btn>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<script>
export default {
  props: ["numbers", "operations"],

  data() {
    return {
      currentNumber: "",
      prevNumber: "",
      currentOperation: "",
      prevOperation: ""
    };
  },

  methods: {
    clear() {
      console.log("Clear");
      this.currentNumber = "";
      this.prevNumber = "";
      this.currentOperation = "";
      this.prevOperation = "";
    },
    addNumber(number) {
      if (number !== "=" && number !== "." && this.currentNumber.length <= 12) {
        this.currentNumber += number;
      } else if (number === ".") {
        if (this.currentNumber.includes(".")) {
          return;
        } else {
          this.currentNumber += number;
        }
      } else {
        this.prevOperation = this.currentOperation;
      }
    },
    changeOperation(operation) {
      if (this.currentOperation === "") {
        this.prevNumber = this.currentNumber;
        this.currentNumber = "";
        this.currentOperation = operation;
      } else if (this.prevOperation === "") {
        this.prevOperation = this.currentOperation;
        this.currentOperation = operation;
      }
    }
  },

  watch: {
    prevOperation() {
      if (this.prevOperation !== "") {
        console.log("watch prevOperation");
        switch (this.prevOperation) {
          case "+":
            this.prevNumber = Number(this.prevNumber) + Number(this.currentNumber);
            break;
          case "-":
            this.prevNumber = Number(this.prevNumber) - Number(this.currentNumber);
            break;
          case "*":
            this.prevNumber = Number(this.prevNumber) * Number(this.currentNumber);
            break;
          case "/":
            if (this.currentNumber !== "0") {
              this.prevNumber = Number(this.prevNumber) / Number(this.currentNumber);
            } else {
              this.prevNumber = "Error";
            }
            break;
        }
        this.prevOperation = "";
        this.currentNumber = "";
      }
    }
  }
};
</script>

<style scoped>
p {
  height: 50px;
  text-align: right;
  display: block;
  width: 100%;
  margin: 0 !important;
  padding: 10px 20px 0 0;
}
.clear {
  top: 41px;
  left: 1px;
}
</style>
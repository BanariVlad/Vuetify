<template>
  <div class="d-flex" style="height: 100vh">
    <v-container 
      class="align-self-center" 
      style="width: 300px"
    >
      <v-row>
        <p class="subheading text-right">20 + 107</p>
        <p class="display-1 text-right">127</p>
      </v-row>
      <v-row class="cyan white--text">
        <v-col 
          v-for="operation in operations" 
          :key="operation"
          class="text-center"
        >
          <button class="button">{{operation}}</button>
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
         <button :class='number === numbers[numbers.length - 1] ? "equal" : "button"'>{{number}}</button>
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
      operations: ['/', '*', '-', '+']
    };
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

  .equal {
    background-color: orange;
  }
</style>
<template>
  <v-app>
    <v-content class="teal darken-3">
      <Calculator :numbers="numbers" :operations="operations" />  
    </v-content>
  </v-app>
</template>

<script>

import Calculator from '@/components/Calculator';
export default {
  name: 'App',

  components: {
    Calculator
  },

  data() {
    return {
      numbers: [1, 2, 3, 4, 5, 6, 7, 8, 9, ".", 0, "="],
      operations: ["/", "*", "-", "+"]
    }
  },
};
</script>

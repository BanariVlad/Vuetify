<template>
  <v-app>
    <v-content class="teal">
      <Calculator />  
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

  data: () => ({
    //
  }),
};
</script>

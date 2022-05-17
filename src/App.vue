<template>
  <v-app>
    <RfcView/>
  </v-app>
</template>

<script>
import RfcView from './components/RfcView';

export default {
  name: 'App',

  components: {
    RfcView,
  },

  data: () => ({
    //
  }),
};
</script>

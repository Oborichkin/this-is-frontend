<template>
  <v-app>
    <RfcView/>
  </v-app>
</template>

<script>
// import SearchView from './components/SearchView.vue';
import RfcView from './components/RfcView';

export default {
  name: 'App',

  components: {
    RfcView,
    // SearchView
  },

  data: () => ({
    //
  }),
};
</script>

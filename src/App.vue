<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dark
    >
      <div class="d-flex align-center">
        <v-toolbar-title>Kodo - Search And Filter</v-toolbar-title>
      </div>
    </v-app-bar>

    <v-content>
      <SearchFilter/>
    </v-content>
  </v-app>
</template>

<script>
import SearchFilter from './components/SearchFilter';

export default {
  name: 'App',

  components: {
    SearchFilter,
  },

  data: () => ({
    //
  }),
};
</script>

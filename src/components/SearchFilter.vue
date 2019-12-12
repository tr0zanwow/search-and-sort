<template>
  <v-container>
    <v-layout
      text-center
      wrap
    >
      <v-flex mb-4>
        <h1 class="display-1 font-weight-bold mb-3">
          Welcome to Kodo - Search & Sort Module
        </h1>
        <p class="subheading font-weight-regular">
          This module present's how search via regex works and how data is sorted via some of its common parameters
          <br>To test this search module input some keywords related to the data! By default the result will contain matching query provided
          <br>If you expect an exact match of sentence or word combination please use: For Title:<strong>' title: "search query" '</strong>, For Description:<strong>' description: "search query" '</strong> to get exact result match from data 
        </p>
      </v-flex>
      <v-flex
        xs12
        mb-5
      >
      <v-text-field
              class="mx-4"
              flat
              hide-details
              label="Search"
              prepend-inner-icon="search"
              white
            ></v-text-field>
        <v-layout justify-center>
          
        </v-layout>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
import json_data from '@/assets/mock_data.json'

export default {
  name: 'SearchFilter',
  data (){
    return{
      mock_data: json_data
    }
  }
};
</script>

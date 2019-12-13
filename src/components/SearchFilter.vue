<template>
  <v-container>
    <v-layout
      text-center
      wrap
    >
      <v-flex mb-4>
        <h1 class="display-1 font-weight-bold mb-3">
          Welcome to Kodo - Search &amp; Sort (Module)
        </h1>
        <p class="subheading font-weight-regular">
          This module present's how search via regex works and how data is sorted via filter methods
          <br>To test this search module input some keywords related to the data! As per the assignments goal default the result will contain matching query any where in data
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
              label="Search "
              hint=""
              v-model.lazy="searchFilter"
              prepend-inner-icon="search"
              white
            ></v-text-field>
            <br>
        <v-layout justify-center text-left>
          <v-card>

      <v-card-title>Mock Data<v-spacer></v-spacer><v-card-actions>
              <v-spacer></v-spacer>
              <v-menu offset-y>
      <template v-slot:activator="{ on }">
        <v-btn v-on="on" class="ma-2" text icon color="#1180ef">
        <v-icon>mdi-sort-variant</v-icon>
      </v-btn>
      </template>
      <v-list>
        <v-list-item
          v-for="(item, index) in items"
          :key="index"
          @click="checkFunction(index)"
        >
          <v-list-item-title>{{ item.title }}</v-list-item-title>
        </v-list-item>
      </v-list>
    </v-menu>

              </v-card-actions>
              </v-card-title>
  
    <v-list v-if="searchFilter == ''" three-line class="customList">
      <template v-for="(item, index) in mock_data">
        <v-list-item 
          :key="index"
        >
          <v-list-item-avatar>
            <v-img :src="item.image"></v-img>
          </v-list-item-avatar>

          <v-list-item-content>
            <v-list-item-title v-html="item.name"></v-list-item-title>
            <v-list-item-subtitle v-html="item.description"></v-list-item-subtitle>
          </v-list-item-content>
        </v-list-item>
         <v-divider
          :key="item.name"
          :inset="true"
        ></v-divider>
      </template>
    </v-list>

    <v-list v-else-if="sorted_mock_data_alpha" three-line class="customList">
      <template v-for="(item, index) in sortedMockDataAplha">
        <v-list-item 
          :key="index"
        >
          <v-list-item-avatar>
            <v-img :src="item.image"></v-img>
          </v-list-item-avatar>

          <v-list-item-content>
            <v-list-item-title v-html="item.name"></v-list-item-title>
            <v-list-item-subtitle v-html="item.description"></v-list-item-subtitle>
          </v-list-item-content>
        </v-list-item>
         <v-divider
          :key="item.name"
          :inset="true"
        ></v-divider>
      </template>
    </v-list>

    <v-list v-else-if="sorted_mock_data_date" three-line class="customList">
      <template v-for="(item, index) in sortedMockDataDate">
        <v-list-item 
          :key="index"
        >
          <v-list-item-avatar>
            <v-img :src="item.image"></v-img>
          </v-list-item-avatar>

          <v-list-item-content>
            <v-list-item-title v-html="item.name"></v-list-item-title>
            <v-list-item-subtitle v-html="item.description"></v-list-item-subtitle>
          </v-list-item-content>
        </v-list-item>
         <v-divider
          :key="item.name"
          :inset="true"
        ></v-divider>
      </template>
    </v-list>

    <v-list v-else three-line class="customList">
      <template v-for="(item, index) in getFilteredMockData">
        <v-list-item 
          :key="index"
        >
          <v-list-item-avatar>
            <v-img :src="item.image"></v-img>
          </v-list-item-avatar>

          <v-list-item-content>
            <v-list-item-title v-html="item.name"></v-list-item-title>
            <v-list-item-subtitle v-html="item.description"></v-list-item-subtitle>
          </v-list-item-content>
        </v-list-item>
         <v-divider
          :key="item.name"
          :inset="true"
        ></v-divider>
      </template>
    </v-list>
  </v-card>
  
        </v-layout>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<style scoped>
.customList{
  height: 50vh;
  overflow-x: hidden;
  overflow-y: auto;

}
::-webkit-scrollbar {
    display: block;
    width: 10px;
}
::-webkit-scrollbar-track {
    background-color: rgba(245, 245, 245, 0.568);
    -webkit-border-radius: 10px;
    border-radius: 10px;
}
::-webkit-scrollbar-thumb {
    -webkit-border-radius: 10px;
    border-radius: 10px;
    background: #1180ef; 
}
</style>
<script>
import json_data from '@/assets/mock_data.json'

export default {
  name: 'SearchFilter',
  data (){
    return{
      searchFilter: '',
      filtered_mock_data: [],
      mock_data: json_data,
      sorted_mock_data_alpha: false,
      items: [
        { title: 'Sort Title Alphabetically'},
        { title: 'Sort By Date'}
      ]
    }
  },
  computed: {
    getFilteredMockData(){
      if(this.searchFilter.toLowerCase().includes("title:")){
          var searchTextTitle = this.searchFilter.toString().match(/(?:"[^"]*"|^[^"]*$)/)[0].replace(/"/g, "");

      return this.mock_data.filter((mockData) => {
         if(mockData.name.toLowerCase().indexOf(searchTextTitle) == -1){
            return false
          }
          else{
            return true
          }
      });
      }
      else if(this.searchFilter.toLowerCase().includes("description:")){
          var searchTextDescrip = this.searchFilter.toString().match(/(?:"[^"]*"|^[^"]*$)/)[0].replace(/"/g, "");

      return this.mock_data.filter((mockData) => {
         if(mockData.description.toLowerCase().indexOf(searchTextDescrip) == -1){
            return false
          }
          else{
            return true
          }
      });
      }
      else{
        return this.mock_data.filter((mockData) => {
        return this.searchFilter.toLowerCase().split(' ').every(searchText => mockData.name.toLowerCase().includes(searchText)) || this.searchFilter.toLowerCase().split(' ').every(searchText => mockData.description.toLowerCase().includes(searchText));
      });
      }
    }
  },
  created(){
  },
  methods:{
     sortedMockDataAplha(){
       var tempDataForSortAlpha = this.mock_data
      function compare(a,b){
        if (a.name < b.name)
          return -1;
        if (a.name > b.name)
          return 1;
        return 0;
      }
      return tempDataForSortAlpha.sort(compare);
    },
    checkFunction(val){
      if(val==0){
        return this.sortDataAplha()
      }
      else{
        return this.sortDataByTime()
      }
    },
    sortDataAplha(){
      this.sorted_mock_data_alpha=true
      this.sortedMockDataAplha()
    },
    sortDataByTime(){
      this.sorted_mock_data=true
      this.sortedMockDataDate()
    },
    sortedMockDataDate(){
      var tempDataForSortDate = this.mock_data
      return tempDataForSortDate.sort((a, b) => Date.parse(a.dateLastEdited) - Date.parse(b.dateLastEdited))
    }
  },
  watch: {
    searchFilter() {
      this.sorted_mock_data_alpha=false
      this.sorted_mock_data=false
    },
  },
};
</script>

<template>
  <div class="home">
    <div>
      <b-jumbotron bg-variant="info" text-variant="white" border-variant="dark">
        <template slot="header">What's Trending</template>
        <p id="message">Search to find out what's trending</p>
        <template>
          <form>
            <input type="text" v-model="search.userInput" />
            <br />
            <button type="submit" class="btn btn-primary" @click.prevent="handleSubmit">Trending</button>
            <!-- <button type="clear" class="btn btn-primary clear" @click="clear">Clear</button> -->
          </form>
        </template>
      </b-jumbotron>
      <div id="searchResult" v-for="(result,index) in search.results" v-bind:key="index">
        <h2>{{search.results[index].title}}</h2>
        <p>{{search.results[index].snippet}}</p>
        <a :href="search.results[index].link">
          {{search.results[index].link}}
        </a>
       
      </div>
    </div>
  </div>
</template>

// <script>
// @ is an alias to /src
import axios from "axios";
export default {
  // el: '#search',
  data() {
    return {
      search: {
        userInput: "",
        googleKey: "AIzaSyBRlj_omJsZWTgEIXq9yLePCL_HNfIfdkk",
        results: []
      }
    };
  },
  methods: {
    handleSubmit() {
      axios
        .get(
          "https://www.googleapis.com/customsearch/v1?key=" +
            this.search.googleKey +
            "&cx=015376139325119918930:rwhxpl8byui&q=" +
            this.search.userInput
        )
        .then(response => {
          console.log(this.search.userInput);
          console.log(response.data);
          this.search.results = response.data.items;
          console.log(this.search.results);
        });
    }
  }
};
</script>
<style scoped>
#searchResult{
  text-align: left;
}
</style>


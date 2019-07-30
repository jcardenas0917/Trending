<template>
  <div class="home">
    <div>
      <b-jumbotron bg-variant="info" text-variant="white" border-variant="dark">
        <template slot="header">What's Trending</template>
        <p id = "message">Search to find out what's trending</p>
        <template>
          <form>
            <input type="text" v-model="search.userInput" />
            <br />
            <button type="submit" class="btn btn-primary" @click.prevent="handleSubmit">Trending</button>
            <!-- <button type="clear" class="btn btn-primary clear" @click="clear">Clear</button> -->
            <div id = "searchResult">
           
             
          </div>
          </form>
          
        </template>

        <hr class="my-4" />
      </b-jumbotron>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import axios from "axios";
export default {
  data() {
    return {
      search: {
        userInput: "",
        googleKey:"AIzaSyBRlj_omJsZWTgEIXq9yLePCL_HNfIfdkk",
        googleSearch : "https://www.googleapis.com/customsearch/v1?key=" + this.googleKey + "&cx=015376139325119918930:rwhxpl8byui&q=" + this.searchInput,
        replace : this.googleSearch.replace(" ", "%20")
      }
    };
  },
  methods: {
    handleSubmit() {
      axios
        .get(
         this.replace
        )
        .then(response => {
          console.log(response);
       
        });
    },

  }
};
</script>

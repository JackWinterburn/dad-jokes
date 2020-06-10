<template>
  <div>
    <SearchJokes v-on:search-text="searchText" />
    <Joke
     v-for="joke in jokes" 
     :key="joke.id"
     :joke="joke.joke"
     :id="joke.id"
     />
  </div>
</template>

<script>
import axios from "axios";
import SearchJokes from "../../components/SearchJokes"
import Joke from "../../components/Joke"

export default {
  components:{
    Joke,
    SearchJokes
  },

  head(){
    return{
      title: "Dad Jokes",
      meta: [{
        hid: "description",
        name: "description",
        content: "Best place for corny dad jokes"
        }],
    }
  },

  data(){
    return{
      jokes: [],
    }
  },

  async created(){
    const config = {
      headers: {
        "Accept": "application/json"
      }
    };

    try{
      const res = await axios.get(
        "https://icanhazdadjoke.com/search", config
      );
      this.jokes = res.data.results
    }catch(err){
      console.log(err)
    };
  },

  methods:{
   async  searchText(text){
      const config = {
      headers: {
        "Accept": "application/json"
      }
    };

    try{
      const res = await axios.get(
        `https://icanhazdadjoke.com/search?term=${text}`, config
      );
      this.jokes = res.data.results
    }catch(err){
      console.log(err)
    };
    }
  },
}
</script>

<style>

</style>
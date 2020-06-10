<template>
  <div>
    <nuxt-link to="/jokes">
    Back to List view
    </nuxt-link>  
    <h2>{{ joke }}</h2>
    <hr>
    <small>Joke ID: {{ $route.params.id }}</small>
  </div>
</template>

<script>
import axios from "axios";

export default {
  head(){
    return{
      title: this.headTitle
    }
  },

  data(){
    return{
      joke: {},
      headTitle: "",
    }
  },

  async created(){
    const config = {
      headers: {
        "Accept": "application/json",
      }
    };

  try{
    const res = await axios.get(
      `https://icanhazdadjoke.com/j/${this.$route.params.id}`, config
    );
    this.joke = res.data.joke;
    this.headTitle = res.data.joke.substring(0, 14) + "..."
  }catch(err){
    console.log(err);
  };
  }
};
</script>

<style>

</style>
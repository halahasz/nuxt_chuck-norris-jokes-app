<template>
  <div>
    <SearchJokes v-on:search-text="searchText" />
    <Joke
      :key="joke.id"
      v-for="joke in jokes"
      :id="joke.id"
      :joke="joke.joke"
    />
  </div>
</template>

<script>
import axios from "axios";
import Joke from "../../components/Joke";
import SearchJokes from "../../components/SearchJokes";

export default {
  components: {
    Joke,
    SearchJokes
  },
  data() {
    return {
      jokes: []
    };
  },
  async created() {
    const config = {
      headers: {
        Accept: "application/json"
      }
    };
    try {
      const res = await axios.get(
        "https://api.icndb.com/jokes/random/5",
        config
      );
      this.jokes = res.data.value;
      console.log(res.data.value);
    } catch (err) {
      console.log(err);
    }
  },
  methods: {
    async searchText(text) {
      const config = {
      headers: {
        Accept: "application/json"
      }
    };
    try {
      const res = await axios.get(
        "https://api.icndb.com/jokes",
        config
      );
      this.jokes = res.data.value.filter(a => a.joke.toLowerCase().split(' ').includes(text))
    } catch (err) {
      console.log(err);
    }
    }
  },
  head() {
    return {
      title: "Chuck Norris jokes",
      meta: [
        {
          hid: "description",
          name: "description",
          content: "Best place for Chuck Norris jokes"
        }
      ]
    };
  }
};
</script>

<style></style>

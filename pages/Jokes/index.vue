<template>
  <div>
    <SearchJokes v-on:search-text="searchText" />
    <Joke
      :key="joke.id"
      v-for="joke in jokes"
      :id="joke.id"
      :joke="joke.joke"
    />
    <p class="noJokes" v-if="jokes.length === 0">
      There is no joke to match this term
    </p>
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
      let newJokes = res.data.value.map(joke => ({
        id: joke.id,
        joke: joke.joke.replace(/&quot;/g, '"')
      }));
      this.jokes.push(...newJokes);
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
        const res = await axios.get("https://api.icndb.com/jokes", config);
        const resRand = await axios.get(
          "https://api.icndb.com/jokes/random/5",
          config
        );
        const newJokes = res.data.value.map(joke => ({
          id: joke.id,
          joke: joke.joke.replace(/&quot;/g, '"')
        }));
        const newJokesRand = resRand.data.value.map(joke => ({
          id: joke.id,
          joke: joke.joke.replace(/&quot;/g, '"')
        }));
        text.length > 0
          ? (this.jokes = newJokes.filter(joke => ({
              id: joke.id,
              joke: joke.joke
                .toLowerCase()
                .split(" ")
                .includes(text)
            })))
          : (this.jokes = newJokes);
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

<style>
.noJokes {
  color: rgb(115, 121, 150);
  text-align: center;
  font-size: 18px;
  padding: 40px 15px;
}
</style>

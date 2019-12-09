<template>
  <div>
    <nuxt-link to="/jokes">Back to jokes</nuxt-link>
    <h2>{{ joke }}</h2>
    <hr />
    <small>Joke id: {{ $route.params.id }}</small>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      joke: {}
    };
  },
  head() {
    return {
      title: "Joke",
      meta: [
        {
          hid: "description",
          name: "description",
          content: "Best place for Chuck Norris jokes"
        }
      ]
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
        `https://api.icndb.com/jokes/${this.$route.params.id}`,
        config
      );
      this.joke = res.data.value.joke;
    } catch (err) {
      console.log(err);
    }
  }
};
</script>

<style></style>

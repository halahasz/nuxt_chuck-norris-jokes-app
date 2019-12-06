<template>
  <div>jokes</div>
</template>

<script>
import axios from "axios";

export default {
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
      const res = await axios.get("http://api.icndb.com/jokes/random/10", config);
      this.jokes = res.data.value;
    } catch (err) {
      console.log(err);
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

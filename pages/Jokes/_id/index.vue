<template>
  <div>
    <nuxt-link to="/jokes">Back to jokes</nuxt-link>
    <h2>{{ joke }}</h2>
    <div class="hr"></div>
    <small>Joke id: {{ $route.params.id }}</small>
  </div>
</template>

<script>
import axios from "axios";
const url = "https://api.icndb.com/jokes";

export default {
  data() {
    return {
      joke: ''
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
        `${url}/${this.$route.params.id}`,
        config
      );
      this.joke = res.data.value.joke.replace(/&quot;/g,'"');
      conslole.log(this.joke)
    } catch (err) {
      console.log(err);
    }
  }
};
</script>

<style>
h2 {
  color: rgb(115, 121, 150);
  text-align: center;
  font-size: 18px;
  padding: 30px 15px;
}
.nuxt-link-active {
  color: rgb(31, 21, 146);
  box-shadow: 0 5px 20px -5px rgb(149, 170, 228);
  display: inline-block;
  padding: .3rem 1rem;
  border-radius: 5px;
  transition: all .2s ease-in-out;
}
.nuxt-link-active:hover {
  background: rgb(155, 179, 223);
  color: #fff;
  margin-right: .5rem;
}
.hr {
  height: 1px;
  width: 100%;
  background-color: rgb(184, 224, 181);
}

</style>

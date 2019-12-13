<template>
  <div>
    <SearchJokes v-on:search-text="searchText" />
    <transition-group name="list-animation">
      <Joke
        :key="joke.id"
        v-for="joke in jokes"
        :id="joke.id"
        :joke="joke.joke"
      />
    </transition-group>
    <p class="noJokes" v-if="jokes == 'noJokes'">
      There is no jokes matching this term
    </p>
    <div class="lds-roller" :busy="isBussy" v-if="isBussy">
      <div></div>
      <div></div>
      <div></div>
      <div></div>
      <div></div>
      <div></div>
      <div></div>
      <div></div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Joke from "../../components/Joke";
import SearchJokes from "../../components/SearchJokes";
const url = "https://api.icndb.com/jokes";

export default {
  components: {
    Joke,
    SearchJokes
  },
  data() {
    return {
      jokes: [],
      test: [],
      isBussy: true
    };
  },
  async created() {
    const config = {
      headers: {
        Accept: "application/json"
      }
    };
    try {
      const res = await axios.get(`${url}/random/5`, config);
      let newJokes = res.data.value.map(joke => ({
        id: joke.id,
        joke: joke.joke.replace(/&quot;/g, '"')
      }));
      this.jokes.push(...newJokes);
    } catch (err) {
      console.log(err);
    }
    this.isBussy = false;
  },
  methods: {
    async searchText(text) {
      const config = {
        headers: {
          Accept: "application/json"
        }
      };

      try {
        const res = await axios.get(url, config);
        const resRand = await axios.get(`${url}/random/5`, config);
        const newJokes = res.data.value.map(joke => ({
          id: joke.id,
          joke: joke.joke.replace(/&quot;/g, '"')
        }));
        this.jokes = newJokes;
        const newJokesRand = resRand.data.value.map(joke => ({
          id: joke.id,
          joke: joke.joke.replace(/&quot;/g, '"')
        }));
        var re = new RegExp(text, 'gi');
        const filterJokes = newJokes.filter(joke =>
          joke.joke
            .toLowerCase()
            .match(re)
        );
        text.length > 0 && filterJokes.length > 0
          ? (this.jokes = filterJokes)
          : text.length > 0
          ? (this.jokes = "noJokes")
          : (this.jokes = newJokesRand);
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
.list-animation-enter,
.list-animation-leave-to {
  opacity: 0;
  transform: translateY(30px);
}

.list-animation-leave-active {
  position: absolute;
  width: 100%;
}
@media screen and (max-width: 800px) {
  .list-animation-leave-active {
    width: 800vw;
  }
}
.noJokes {
  color: rgb(115, 121, 150);
  text-align: center;
  font-size: 18px;
  padding: 40px 15px;
}

/* loader */
.lds-roller {
  margin: 0 auto;
  transform: scale(0.6);
  position: relative;
  width: 80px;
  height: 80px;
}
.lds-roller div {
  animation: lds-roller 1.2s cubic-bezier(0.5, 0, 0.5, 1) infinite;
  transform-origin: 40px 40px;
}
.lds-roller div:after {
  content: " ";
  display: block;
  position: absolute;
  width: 7px;
  height: 7px;
  border-radius: 50%;
  background: rgb(155, 179, 223);
  margin: -4px 0 0 -4px;
}
.lds-roller div:nth-child(1) {
  animation-delay: -0.036s;
}
.lds-roller div:nth-child(1):after {
  top: 63px;
  left: 63px;
}
.lds-roller div:nth-child(2) {
  animation-delay: -0.072s;
}
.lds-roller div:nth-child(2):after {
  top: 68px;
  left: 56px;
}
.lds-roller div:nth-child(3) {
  animation-delay: -0.108s;
}
.lds-roller div:nth-child(3):after {
  top: 71px;
  left: 48px;
}
.lds-roller div:nth-child(4) {
  animation-delay: -0.144s;
}
.lds-roller div:nth-child(4):after {
  top: 72px;
  left: 40px;
}
.lds-roller div:nth-child(5) {
  animation-delay: -0.18s;
}
.lds-roller div:nth-child(5):after {
  top: 71px;
  left: 32px;
}
.lds-roller div:nth-child(6) {
  animation-delay: -0.216s;
}
.lds-roller div:nth-child(6):after {
  top: 68px;
  left: 24px;
}
.lds-roller div:nth-child(7) {
  animation-delay: -0.252s;
}
.lds-roller div:nth-child(7):after {
  top: 63px;
  left: 17px;
}
.lds-roller div:nth-child(8) {
  animation-delay: -0.288s;
}
.lds-roller div:nth-child(8):after {
  top: 56px;
  left: 12px;
}
@keyframes lds-roller {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
</style>

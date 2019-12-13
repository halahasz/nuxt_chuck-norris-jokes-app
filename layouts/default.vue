<template>
  <div class="wrapper">
    <div class="container">
      <AppHeader />
      <nuxt />
    </div>
  </div>
</template>

<script>
import AppHeader from "../components/AppHeader";

export default {
  components: {
    AppHeader
  }
};
</script>

<style>
@import url("https://fonts.googleapis.com/css?family=Lato|Open+Sans&display=swap");
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: "Open Sans", sans-serif;
  font-size: 1rem;
  line-height: 1.6;
  background: #f4f4f4;
}
a {
  color: #666;
  text-decoration: none;
}
ul {
  list-style: none;
}
.wrapper {
  padding: 1rem 2rem;
  background: #fff;
  max-width: 800px;
  margin: 2rem auto;
}
.container {
  position: relative;
}
@media screen and (max-width: 800px) {
  body {
    background: #fff
  }
  .wrapper {
    margin: 0 auto;
  }
}
</style>

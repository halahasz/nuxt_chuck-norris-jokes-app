<template>
  <div>
    <h1>
      Welcome to the Chuck Norris jokes app
    </h1>
  </div>
</template>

<script>
export default {
  head() {
    return {
      title: "Welcome to Chuck Norris jokes app",
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
h1 {
  color: rgb(115, 121, 150);
  text-align: center;
  font-size: 25px;
  padding: 30px 15px 50px;
}
</style>

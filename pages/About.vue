<template>
  <div>
    <h1>About Chuck Norris jokes</h1>
    <p class="desc">This is an app that displays Chuck Norris jokes</p>
  </div>
</template>

<script>
export default {
  head() {
    return {
      title: "About The App",
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
.desc {
  color: rgb(115, 121, 150);
  text-align: center;
  font-size: 18px;
  padding: 0px 15px 50px;
}
</style>

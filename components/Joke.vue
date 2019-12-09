<template>
  <nuxt-link :to="`jokes/${id}`">
    <div class="joke">
      <p>{{ joke }}</p>
    </div>
  </nuxt-link>
</template>

<script>
export default {
  name: "Joke",
  props: ["joke", "id"]
};
</script>

<style>
.joke {
  padding: 1rem;
  border: 1px solid  rgba(149, 170, 228, .3);
  margin: 1rem 0;
  border-radius: 5px;
  box-shadow: 0 5px 10px -5px rgba(170, 227, 241, 0.4);
}
</style>

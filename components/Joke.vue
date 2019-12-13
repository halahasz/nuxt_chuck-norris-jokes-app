<template>
  <nuxt-link :to="`jokes/${id}`" class="block animated">
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

<style scoped>
.animated {
  transition: all 0.7s;
  max-width: 100%
}
.joke {
  padding: 1rem;
  border: 1px solid rgba(149, 170, 228, 0.3);
  margin: 1rem auto;
  border-radius: 5px;
  box-shadow: 0 5px 10px -5px rgba(170, 227, 241, 0.4);
}
.appear-joke {
  animation: bounce-in 0.8s ease-in-out;
}
.block {
  display: block;
}
@keyframes bounce-in {
  0% {
    transform: translateY(15px);
  }
  100% {
    transform: translateY(0);
  }
}
</style>

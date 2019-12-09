<template>
  <header class="header">
    <h1 class="title">Chuck Norris jokes</h1>
    <ul>
        <li>
            <nuxt-link to="/">Home</nuxt-link>
        </li>
        <li>
            <nuxt-link to="/jokes">Jokes</nuxt-link>
        </li>
        <li>
            <nuxt-link to="/about">About</nuxt-link>
        </li>
    </ul>
  </header>
</template>

<script>
export default {
  name: 'AppHeader'
};
</script>

<style>
.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 1rem;
  padding-bottom: 1rem;
  border-bottom: 1px solid rgb(184, 224, 181);
}
.header .title {
  font-family: 'Lato', sans-serif;
  font-size: 3rem;
  color:rgb(69, 78, 119);
  font-weight: 700;
}
.header ul {
  display: flex;
}
.header a {
  display: inline-block;
  background: rgb(155, 179, 223);
  color: #fff;
  padding: .3rem 1rem;
  margin-right: .5rem;
  border-radius: 5px;
  border: 1px solid rgb(155, 179, 223);
  transition: all .2s ease-in-out;
}
.header a:hover {
  border: 1px solid rgb(120, 117, 150);
  background: transparent;
  color: rgb(120, 117, 150);
  box-shadow: 0 5px 20px -5px rgb(149, 170, 228);
}
</style>

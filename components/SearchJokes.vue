<template>
  <form @submit.prevent="onSubmit">
    <input type="text" v-model="text" placeholder="Search term
    ..." />
    <input type="submit" value="Search jokes" />
  </form>
</template>

<script>
export default {
  name: "SearchJokes",
  data() {
    return {
      text: ""
    };
  },
  methods: {
    onSubmit() {
      this.$emit("search-text", this.text.toLowerCase());
      this.text = "";
    }
  }
};
</script>

<style>
input {
  border: 1px solid rgb(179, 218, 176);
  padding: 10px;
  border-radius: 5px;
}
input:focus, input:active {
  outline: none;
  box-shadow: 0 5px 15px -7px rgb(184, 224, 181);
}
input[type="submit"] {
  background:rgb(179, 218, 176);
  color: white;
  cursor: pointer;
  margin-left: 10px;
  transition: all .2s ease-in-out;
}
input[type="submit"]:hover {
  background:transparent;
  border: 1px solid rgb(149, 194, 147);
  color: rgb(69, 78, 119);
  box-shadow: 0 5px 15px -7px rgb(184, 224, 181);
}
</style>

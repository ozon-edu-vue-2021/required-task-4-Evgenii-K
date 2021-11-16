<template>
  <div id="app">
    <Form />
  </div>
</template>

<script>
import Form from "./components/Form/Form.vue";

export default {
  name: "App",
  components: {
    Form,
  },
};
</script>

<style>
#app {
  display: grid;
  justify-content: center;
  align-items: start;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  color: #2c3e50;
  background-color: #fafafa;
  padding: 24px;
  box-sizing: border-box;
}

html,
body,
#app {
  height: 100%;
}

input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
    /* display: none; <- Crashes Chrome on hover */
    -webkit-appearance: none;
    margin: 0; /* <-- Apparently some margin are still there even though it's hidden */
}

* {
  box-sizing: border-box;
}
</style>

<template>
  <div class="hello">
    <h1>What is Lorem Ipsum??</h1>
    <p>Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book. It has survived not only five centuries, but also the leap into electronic typesetting, remaining essentially unchanged. It was popularised in the 1960s with the release of Letraset sheets containing Lorem Ipsum passages, and more recently with desktop publishing software like Aldus PageMaker including versions of Lorem Ipsum.</p>
    <router-link to="/questions" class="start" tag="button">Start</router-link>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  data() {
    return {
      msg: "Welcome to Your Vue.js App"
    };
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1,
h2 {
  font-weight: bold;
}
ul {
  list-style-type: none;
  padding: 0;
}
.start {
  background-color: tomato;
  height: 50px;
  width: 80px;
  border-radius: 10px;
  margin-top: 20px;
}
.hello {
  text-align: center;
  padding: 30px 200px;
}
</style>

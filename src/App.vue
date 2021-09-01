<template>
  <div class="container">
    <Header :showTask="showTask" @toggle-add-task="toggleAddTask" title="Task Tracker" />
    <router-view :showTask="showTask"></router-view>
    <small> Double Click To Mark As Done </small>
    <Footer />
  </div>
</template>

<script>
import Home from "./views/Home.vue";
import About from "./views/About.vue";
import Header from "./components/Header.vue";
import Footer from "./components/Footer.vue";

export default {
  name: 'App',
  components: {
    Home,
    About,
    Header,
    Footer,
  },
  data () {
    return {
      showTask: false,
    }
  },
  methods: {
    toggleAddTask() {
      this.showTask = !this.showTask
    },
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap');
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: 'Poppins', sans-serif;
}
.container {
  max-width: 500px;
  margin: 30px auto;
  overflow: auto;
  min-height: 300px;
  border: 1px solid steelblue;
  padding: 30px;
  border-radius: 5px;
}
.btn {
  display: inline-block;
  background: #000;
  color: #fff;
  border: none;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 15px;
  font-family: inherit;
}
.btn:focus {
  outline: none;
}
.btn:active {
  transform: scale(0.98);
}
.btn-block {
  display: block;
  width: 100%;
}
</style>

<template>
  <div id="app" class="container">
    <ListTasks></ListTasks>
  </div>
</template>

<script>
import ListTasks from './components/Tasks/ListTasks'
export default {
  name: 'app',
  components: {
    ListTasks
  }
}

</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  background-color: lightblue;
  border-radius: 2rem;
  border: 1px solid lightblue;
  margin-top: 20px;

}

h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>

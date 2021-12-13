<template>
  <div class="container">
    <div class="row">
      <Navigation />
        <div v-for="(user, key) in users" :key="key">
          <!-- <p>Image</p>
          <p>{{ user.name }}</p>
          <p>{{ user.username }}</p> -->
            id: {{ user.id }}<br>
name: {{ user.name }}

{{users}}
        </div>
      <!-- <span>{{user.name}}</span>
      <p>{{user.username}}</p>  -->
        <!-- id: {{ user.id }}<br> -->
        <!-- name: {{ user.name }} -->
    </div>
  </div>
</template>

<script>
import Navigation from "./components/Navigation.vue";
export default {
  name: "App",
  components: {
    Navigation,
  },
  data() {
    return {
      users_api: "https://jsonplaceholder.typicode.com/users",
      user: {},
    };
  },
  created() {
    fetch(`${this.users_api}`)
      .then((res) => {
        return res.json();
      })
      .then(this.setUsers);
  },
  methods: {
    setUsers(results) {
      this.users = results;
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

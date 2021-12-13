<template>
  <div class="container">
    <div class="row">
      <Navigation />
      <div class="col-9 d-flex flex-wrap">
        <div v-for="user in users" v-bind:key="user.id" class="col-4">
          <img src="https://fakeimg.pl/300/" alt="" />
          <p>{{ user.name }}</p>
          <p>{{ user.username }}</p>
        </div>
      </div>
      <!-- <div v-for="(user, key) in users" :key="key">
            {{user[0].name}}
        </div> -->
    </div>
    <!-- <span>{{user.name}}</span>
      <p>{{user.username}}</p>  -->
    <!-- id: {{ user.id }}<br> -->
    <!-- name: {{ user.name }} -->
    <div class="row">
      
      <!-- <div class="user-details d-flex"> -->
        
      <!-- </div> -->
    </div>
    
  </div>
</template>

<script>
import Navigation from "./components/Navigation.vue";
import axios from "axios";
export default {
  name: "App",
  components: {
    Navigation,
  },
  data() {
    return {
      users_api: "https://jsonplaceholder.typicode.com/users",
      users: [],
    };
  },
  // created() {
  //   fetch(`${this.users_api}`)
  //     .then((res) => {
  //       return res.json();
  //     })
  //     .then(this.setUsers);
  // },
  // mounted () {
  //   axios.get('https://jsonplaceholder.typicode.com/users').then(response => (this.user = response.data)).catch(error => console.log(error))
  // },
  mounted() {
    axios
      .get(this.users_api)
      .then(({ data }) => {
        this.users = data;
      })
      .catch((e) => {
        console.log(e);
      });
  },
  // methods: {
  //   setUsers(results) {
  //     this.user = results;
  //   },
  // },
};
</script>

<style>
#app {
  /* font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px; */
}
</style>

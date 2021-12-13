<template>
<div class="container">
  <div class="row">
    <div class="col-12 d-flex flex-wrap">
        <div v-for="user in users" v-bind:key="user.id" class="col-4">
          <img src="https://fakeimg.pl/300/" alt="" />
          <p>{{ user.name }}</p>
          <p>{{ user.username }}</p>
        </div>
    </div>
  </div>
</div>
</template>

<script>
import axios from "axios";
export default {
  name: "App",
  data() {
    return {
      users_api: "https://jsonplaceholder.typicode.com/users",
      users: [],
    };
  },
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
};
</script>

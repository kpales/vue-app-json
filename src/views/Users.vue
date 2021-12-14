<template>
  <div class="container">
    <div class="row">
      <div class="col-12 d-flex flex-wrap">
        <div v-for="user in users" v-bind:key="user.id" class="col-3 my-2">
          <UsersDetail
            :user-id = user.id
            :user-name = user.username
            :user-fullName = user.name
           />
        </div>

        <!-- <div v-for="user in users" v-bind:key="user.id" class="col-12 col-lg-4">
          <a v-bind:href="'https://jsonplaceholder.typicode.com/users/' + user.id + '/albums'">
          <img src="https://fakeimg.pl/300/" alt="" />
          <p>{{ user.name }}</p>
          <p>{{ user.username }}</p>
          </a>
        </div> -->
      </div>
    </div>
  </div>
</template>

<script>
import UsersDetail from "@/components/UsersDetail.vue";
import axios from "axios";
export default {
  name: "Users-view",
  components: {
    UsersDetail,
  },
  data() {
    return {
      users_endpoint: "https://jsonplaceholder.typicode.com/users",
      users: [],
      album_endpoint: "https://jsonplaceholder.typicode.com/albums",
      album:[]
    };
  },
  mounted() {
    axios
      .get(this.users_endpoint)
      .then(({ data }) => {
        this.users = data;
      })
      .catch((e) => {
        console.log(e);
      });
          axios
      .get(this.album_endpoint)
      .then(({ data }) => {
        this.album = data;
      })
      .catch((e) => {
        console.log(e);
      });
  }
};

</script>

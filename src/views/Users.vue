<template>
  <div class="container">
    <div class="row">
      <div class="col-12 d-flex flex-wrap">
        <div v-for="user in users" v-bind:key="user.id" class="col-3 my-2">
          <UsersDetail
            :user-id="user.id"
            :user-name="user.username"
            :user-fullName="user.name"
          />
        </div>
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
  },
};
</script>
